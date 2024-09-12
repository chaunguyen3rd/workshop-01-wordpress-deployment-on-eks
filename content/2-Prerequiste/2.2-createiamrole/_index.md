---
title : "Create IAM Role"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

**IAM roles in AWS (Identity and Access Management)** are a way to grant specific permissions to users, services, or applications without using their own identity. Instead of being tied to a single user, IAM roles can be assumed temporarily by trusted entities, allowing them to perform actions based on the permissions associated with the role.

IAM roles are commonly used for:

- **Cross-Account Access**: Allowing users or services in one AWS account to access resources in another account.
- **Service Permissions**: Granting AWS services (like EC2 or Lambda) the necessary permissions to interact with other AWS services.
- **Federated Users**: Granting permissions to users who have been authenticated outside of AWS (e.g., through an external identity provider).
  
IAM roles are defined by a policy that specifies what actions are allowed or denied, and they are assumed by calling the `sts:AssumeRole` API, which provides temporary security credentials for the duration of the session.

### Create IAM Role

In this step, we will proceed to create required IAM Roles and policies to finish this lab. 

### Content
  - [Create labEKSClusterRole](2.2.1-createeksclusterrole/)
  - [Create labNodeGroupsRole](2.2.2-createnodegrouprole/)
  - [Create labEFSCSIDriverRole](2.2.3-createefscsidriverrole/)
