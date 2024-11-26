---
sidebar_position: 2
---

# Import Cluster Template

The "AWS EKS Environment Provider From Existing Cluster" template allows you to set up an EKS runtime for Portage that uses a preexisting EKS cluster. 

Here are the 2 main uses:

1. Use a cluster you had set up in the past, before adopting Portage.
1. Continue using whatever mechanism you prefer to provision your EKS clusters (outside of Portage).
    * For example, you may wish to use [eksctl](https://eksctl.io/) or [Rancher](https://www.rancher.com/) to create your clusters.

Whatever your reason, using this template will allow you to use prexisting clusters as part of an Portage EKS Environment Provider.

:::info
This template only "imports" EKS clusters for use by an EKS Environment Provider. It does NOT import any applications that are running in an imported cluster that were created outside of Portage.
:::

#### Screenshot of the AWS EKS Environment Provider From Existing Cluster Template:
<p align="center">
![eks_existing_cluster.png](/img/opa/providers/eks_existing_cluster.png)
</p>

## How Is This Template Different From The AWS EKS Environment Provider Template?

This template performs a subset of what the "AWS EKS Environment Provider" template does. Please see the [AWS EKS Environment Provider template documentation](newClusterTemplate) for a detailed list of features. The purpose of this template is to use an existing EKS cluster, but to also create the Portage-specific infrastructure that is needed in order for Portage to use the cluster as part of an EKS Environment Provider.

If you use the "AWS EKS Environment Provider From Existing Cluster" template, the following will NOT be created/configured:

  * VPC
  * EKS Cluster
  * FluentBit log forwarding
  * Security Groups
  * OIDC Provider for service accounts
  * IAM Roles
  * aws-auth ConfigMap settings

Choosing to use a cluster that is created outside of Portage means that you are responsible for configuring your cluster to be compatible with Portage. See the [AWS EKS Environment Provider template documentation](newClusterTemplate) for details on what Portage expects to be set up for a cluster. 

### Optional Components

The following will only be created if you answer "Yes" to "Create Portage Resources In EKS Cluster?"
  * "opa-cluster-admin" ClusterRoleBinding
  * ClusterRole for viewing/listing namespaces
