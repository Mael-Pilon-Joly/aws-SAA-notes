# Basics

Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service provided by AWS. It simplifies the process of deploying, managing, and scaling containerized applications using Kubernetes. Here’s a detailed overview of EKS:

Key Features
Managed Kubernetes Control Plane:

Automatic Upgrades: EKS automatically manages the Kubernetes control plane and performs regular upgrades and patching.
High Availability: The control plane is distributed across multiple Availability Zones (AZs) to ensure high availability and fault tolerance.
Integration with AWS Services:

IAM Integration: EKS integrates with AWS Identity and Access Management (IAM) to control access to Kubernetes resources.
Elastic Load Balancing (ELB): Supports both Application Load Balancers (ALB) and Network Load Balancers (NLB) for load balancing.
Amazon RDS & DynamoDB: Easily integrates with AWS databases for application data storage.
Security and Compliance:

VPC Integration: Kubernetes nodes run in an Amazon Virtual Private Cloud (VPC) for network isolation.
Security Groups: Use security groups to control inbound and outbound traffic for your EKS worker nodes.
Encryption: Supports encryption of data at rest and in transit.
Scalability:

# Auto Scaling: 

Supports both Kubernetes Cluster Autoscaler and AWS Auto Scaling to automatically adjust the number of worker nodes based on demand.
Horizontal Pod Autoscaling: Automatically scales the number of pod replicas based on CPU or memory usage.
Monitoring and Logging:

Tools for autoscaling:

Karpenter
Purpose: Karpenter is a high-performance, flexible Kubernetes cluster autoscaler designed to optimize application availability and cluster efficiency.
Functionality:
Right-Sized Resources: It automatically provisions compute resources (such as Amazon EC2 instances) that match the specific needs of your workloads.
Response Time: Karpenter can launch new resources in under a minute, ensuring rapid adaptation to changing application loads.
Integration with AWS: Karpenter integrates closely with AWS services to provide precise resource provisioning based on workload requirements, including compute, storage, acceleration, and scheduling needs.
Support: While Karpenter is fully supported in Amazon EKS, it is also compatible with any Kubernetes cluster that conforms to Kubernetes standards.

Cluster Autoscaler
Purpose: The Cluster Autoscaler is a tool built into Kubernetes that adjusts the number of nodes in your cluster based on the needs of your pods.
Functionality:
Node Management: It automatically scales the number of nodes in an Auto Scaling group up or down when pods fail to schedule or are rescheduled onto other nodes.
Scaling Trigger: The autoscaler triggers scaling actions when it detects that pods cannot be scheduled due to insufficient resources or when there are idle nodes that can be removed.

Comparison
Karpenter (for complex environment, varied type of instance needed):

Provides more granular control over resource provisioning and can handle a wider range of resource types and requirements.
Offers faster response times by provisioning resources within minutes.
It is better suited for dynamic and complex workloads that need fine-tuned resource management.

Cluster Autoscaler (scale based on nodes needs, more stable type of intance):

Works with existing Auto Scaling groups and scales nodes based on the scheduling demands of the pods.
Provides automatic scaling but may not be as responsive or flexible as Karpenter for some use cases.
Use Cases
Karpenter: Ideal for environments requiring high performance and quick adaptation to workload changes, where resource types and configurations vary significantly.
Cluster Autoscaler: Suitable for environments where node scaling is primarily driven by the need to accommodate pod scheduling demands and where the cluster setup is straightforward.

# Amazon CloudWatch:
 Provides monitoring and logging for Kubernetes clusters, including metrics and log aggregation.

# AWS CloudTrail: 
Tracks API calls made to EKS for auditing and compliance.

# Integration with AWS Fargate:

Serverless Compute: Allows running Kubernetes pods on AWS Fargate, which eliminates the need to manage the underlying EC2 instances.
Basic Architecture
Control Plane:

Managed by AWS and includes the Kubernetes API server, etcd (Kubernetes' database), and controllers.
Worker Nodes:

EC2 instances that run the Kubernetes worker nodes and execute containers. These nodes are registered with the EKS control plane.
Amazon EKS Cluster:

Consists of a control plane (managed by AWS) and a set of worker nodes (managed by the user) that run Kubernetes workloads.
Use Cases
Microservices: Ideal for deploying and managing microservices architectures using Kubernetes.
CI/CD Pipelines: Supports continuous integration and continuous deployment (CI/CD) pipelines for automated application delivery.
Data Processing: Suitable for data processing tasks that require scalable and reliable orchestration.

# IAM roles (Granting)

Kubernetes API Endpoint: Each EKS cluster has a Kubernetes API endpoint that users interact with using tools like kubectl.

Identity Types for Access:

IAM Principals (Roles or Users): Users can authenticate to the Kubernetes API using IAM credentials. This is done by signing in to AWS as an IAM user or with federated identities through roles set up by an administrator. This method allows for assigning both Kubernetes permissions and IAM permissions. Kubernetes permissions enable interaction with Kubernetes objects, while IAM permissions control interaction with the Amazon EKS cluster and related AWS resources.

OIDC Provider Users: Users from an external OpenID Connect (OIDC) provider can authenticate to the Kubernetes API. This method only allows for Kubernetes permissions and not IAM permissions for AWS resources.

AWS IAM Authenticator for Kubernetes: This tool on the EKS control plane allows IAM users and roles to access Kubernetes resources in the cluster.

Managing Kubernetes Permissions:

Access Entries: The recommended method for newer clusters is using access entries. This allows management of Kubernetes permissions for IAM principals from outside the cluster using AWS tools like the EKS API, AWS CLI, etc. Access entries offer a centralized and consistent way to manage access using the same tools used for cluster creation.

aws-auth ConfigMap: For older clusters, permissions are managed using the aws-auth ConfigMap inside the cluster. Users can add entries using commands like eksctl create iamidentitymapping. If using this method, it's suggested to migrate to access entries if the cluster's version supports it.

Authentication Modes:

ConfigMap Only: This is the original mode, where the initial cluster creator manages access by editing the aws-auth ConfigMap. Other users can’t modify the initial user’s access.

Both ConfigMap and Access Entries: This mode supports both management methods. However, changes in one method don’t reflect in the other.

Access Entries Only: This mode uses access entries exclusively for managing IAM access to Kubernetes resources, offering granular control with access scopes and policies.

In summary, the article provides guidance on how to configure and manage access to Kubernetes clusters on EKS using IAM and OIDC providers, focusing on flexibility and security in permission assignments.

