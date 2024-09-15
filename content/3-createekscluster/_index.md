---
title : "Create EKS Cluster"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

### Overall
**An Amazon EKS (Elastic Kubernetes Service) cluster** is a managed Kubernetes service that makes it easy to deploy, manage, and scale containerized applications using Kubernetes on AWS. With EKS, AWS handles the management and operation of the Kubernetes control plane, including patching, upgrading, and scaling, allowing you to focus on deploying and managing your applications.

Key features of an EKS cluster include:

- **Managed Kubernetes Control Plane**: AWS manages the highly available Kubernetes control plane, including the API server, etcd, and other critical components.
- **Worker Nodes**: EKS supports both managed and self-managed worker nodes, where the containers run. These nodes can be EC2 instances or AWS Fargate, a serverless compute engine for containers.
Integration with AWS Services: EKS integrates seamlessly with other AWS services like IAM, VPC, ECR, and CloudWatch, providing enhanced security, networking, and monitoring capabilities.
- **High Availability and Scalability**: EKS automatically distributes and replicates the control plane across multiple Availability Zones, ensuring high availability. It also supports automatic scaling of worker nodes.

**EKS** is ideal for running production-grade Kubernetes workloads on AWS, offering a secure, reliable, and scalable environment for containerized applications.

{{% notice info %}}
Read more: https://aws.amazon.com/eks/
{{% /notice %}}

In this step, we will create our EKS Cluster, located in private subnets.

### Content
3.1. [Create EKS cluster](3.1-createekscluster/) \
3.2. [Create Node groups](3.2-createnodegroups/) \
3.3. [Create EFS CSI driver role](3.3-createefscsidriverrole/)