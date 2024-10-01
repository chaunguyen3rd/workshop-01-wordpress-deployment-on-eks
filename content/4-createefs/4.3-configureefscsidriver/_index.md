---
title : "Configure EFS CSI driver"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---

In this step, we will configure our EFS CSI driver.

#### Install **helm**
**Helm** is a package manager for Kubernetes that simplifies the process of deploying and managing applications within a Kubernetes cluster. It uses "charts," which are pre-configured templates that define the structure, dependencies, and configuration options of an application or service.

1. Open your terminal.
    ```
      ssh ubuntu@18.206.88.146 -i ~/.ssh/labBastionHostSSHKey01.pem
    ```
  - Change the ``18.206.88.146`` to your EC2's Public IP address.
  - Change the ``~/.ssh/labBastionHostSSHKey01.pem`` to the path of the Key pair you downloaded when creating your EC2 instance.
  - After successful login to your EC2, switch to sudo user with ``sudo su``.

2. Install **helm**
  - Run this code block
    ```
    curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
    sudo apt-get install apt-transport-https --yes
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
    sudo apt-get update
    sudo apt-get install helm
    ```
  - Confirm the installation with ``helm version``.
    ```
    root@ip-10-0-1-234:~# helm version
    version.BuildInfo{Version:"v3.16.1", GitCommit:"5a5449dc42be07001fd5771d56429132984ab3ab", GitTreeState:"clean", GoVersion:"go1.22.7"}
    root@ip-10-0-1-234:~#
    ```

#### Configure EFS CSI driver
1. Create **efs-csi-controller-sa** service account.
  - Save this **aws-efs-csi-driver-sa.yaml** file.
    + Change ``arn:aws:iam::017820706022:role/labEKSEFSCSIDriverRole`` to your **labEKSEFSCSIDriverRole**'s ARN value.
    ```
    # aws-efs-csi-driver-sa.yaml
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      labels:
        app.kubernetes.io/name: aws-efs-csi-driver
      name: efs-csi-controller-sa
      namespace: kube-system
      annotations:
        eks.amazonaws.com/role-arn: arn:aws:iam::017820706022:role/labEKSEFSCSIDriverRole
    ```
  - Run ``kubectl apply -f aws-efs-csi-driver-sa.yaml``.
    ```
    root@ip-10-0-1-234:~# kubectl get -n kube-system sa | grep efs-csi-controller-sa
    efs-csi-controller-sa                         0         106s
    ```

2. Install the driver using **Helm**
  - Add the Helm repo: ``helm repo add aws-efs-csi-driver https://kubernetes-sigs.github.io/aws-efs-csi-driver/``.
  - Update the repo: ``helm repo update aws-efs-csi-driver``
  - Install a release of the driver using the **Helm** chart.
    ```
    helm upgrade --install aws-efs-csi-driver \
      --namespace kube-system \
      --set controller.serviceAccount.create=false \
      --set controller.serviceAccount.name=efs-csi-controller-sa \
      aws-efs-csi-driver/aws-efs-csi-driver
    ```
  - Check if creation success.
    ```
    root@ip-10-0-1-234:~# helm repo add aws-efs-csi-driver https://kubernetes-sigs.github.io/aws-efs-csi-driver/
    "aws-efs-csi-driver" has been added to your repositories
    root@ip-10-0-1-234:~# helm repo update aws-efs-csi-driver
    Hang tight while we grab the latest from your chart repositories...
    ...Successfully got an update from the "aws-efs-csi-driver" chart repository
    Update Complete. ⎈Happy Helming!⎈
    root@ip-10-0-1-234:~# helm upgrade --install aws-efs-csi-driver \
      --namespace kube-system \
      --set controller.serviceAccount.create=false \
      --set controller.serviceAccount.name=efs-csi-controller-sa \
      aws-efs-csi-driver/aws-efs-csi-driver
    Release "aws-efs-csi-driver" does not exist. Installing it now.
    NAME: aws-efs-csi-driver
    LAST DEPLOYED: Fri Sep 20 13:51:50 2024
    NAMESPACE: kube-system
    STATUS: deployed
    REVISION: 1
    TEST SUITE: None
    NOTES:
    To verify that aws-efs-csi-driver has started, run:

        kubectl get pod -n kube-system -l "app.kubernetes.io/name=aws-efs-csi-driver,app.kubernetes.io/instance=aws-efs-csi-driver"
    root@ip-10-0-1-234:~# kubectl get pod -n kube-system -l "app.kubernetes.io/name=aws-efs-csi-driver,app.kubernetes.io/instance=aws-efs-csi-driver"
    NAME                                 READY   STATUS    RESTARTS   AGE
    efs-csi-controller-5864df9cf-7klcl   3/3     Running   0          16s
    efs-csi-controller-5864df9cf-hslwm   3/3     Running   0          16s
    efs-csi-node-nms8t                   3/3     Running   0          17s
    efs-csi-node-q5tkf                   3/3     Running   0          17s
    root@ip-10-0-1-234:~#
    ```

#### Create Dynamic Provisioning StorageClass
1. Go to [EFS service management console](https://console.aws.amazon.com/efs/home)
  - Click **File systems**.
  - Copy **fs-0003fc3d543db9be6**.
  ![EC2](/images/4.configure/ws01-configure13.png)

2. Create **StorageClass**.
  - Back to your terminal, save this **StorageClass** manifest.
    ```
    # efs-sc.yaml
    kind: StorageClass
    apiVersion: storage.k8s.io/v1
    metadata:
      name: efs-sc
    provisioner: efs.csi.aws.com
    parameters:
      provisioningMode: efs-ap
      fileSystemId: fs-92107410
      directoryPerms: "700"
      gidRangeStart: "1000" # optional
      gidRangeEnd: "2000" # optional
      basePath: "/dynamic_provisioning" # optional
      subPathPattern: "${.PVC.namespace}/${.PVC.name}" # optional
      ensureUniqueDirectory: "true" # optional
      reuseAccessPoint: "false" # optional
    ```
  - Change ``fileSystemId: fs-92107410`` to your FileSystemID from the previous step.
  - Run ``kubectl apply -f efs-sc.yaml``
  - Check if the creation success.
    ```
    root@ip-10-0-1-234:~# kubectl apply -f efs-sc.yaml
    storageclass.storage.k8s.io/efs-sc created
    root@ip-10-0-1-234:~# kubectl get storageclass
    NAME     PROVISIONER             RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
    efs-sc   efs.csi.aws.com         Delete          Immediate              false                  17s
    gp2      kubernetes.io/aws-ebs   Delete          WaitForFirstConsumer   false                  3d20h
    ```

Next, we will configure **labNodeGroupsRole**.