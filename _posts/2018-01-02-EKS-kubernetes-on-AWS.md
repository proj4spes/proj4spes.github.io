---
date: 2018-01-03 09:00:00+00:00
layout: post
title: EKS i.e Kubernetes on AWS
tags:
- Kubernetes
- DevOps
categories:
- Cloud
---


<div class="message">
AWS has announced at the AWS last re:Invent a new product EKS i.e. Elastic Container Service for KUBERNETES to enlarge its offering for the containers world. EKS will be available in preview (1Q of 2018 ?).
</div> 
"<!-- more -->"
Today, customers are running virtually every type of container orchestration and management service on AWS. In addition to Amazon ECS, Kubernetes has also become very popular with AWS customers. A recent survey from the Cloud Native Computing Foundation found that 63 percent of Kubernetes clusters running in the cloud are on AWS, more than any other cloud platform.

Before today, operating Kubernetes with high availability required specialized expertise and a great deal of manual work (see my previous blog ). Customers needed to install and operate Kubernetes masters (which manage a customer’s clusters of servers) across multiple Availability Zones (AZs), replace unhealthy masters, and put measures in place to ensure that updates do not cause application downtime. Amazon EKS removes this complexity, making it easy for customers to run highly available Kubernetes environments. Amazon EKS is the first cloud service to deliver a highly available architecture that automatically distributes Kubernetes masters across multiple AZs to eliminate a single point of failure. This makes it easy for customers to deploy their applications in a highly available fashion. Applications running on Amazon EKS are resilient to the loss of a single master, or even an entire AZ. Amazon EKS automatically detects and replaces unhealthy masters, and it can automatically patch and perform version upgrades for masters.
what are the declared features :
1) security : Integration Kubernetes’ RBAC role with IAM authentication

You can assign RBAC roles directly to each IAM entity (users and ?roles ?) allowing you to granularly control access permissions to your Kubernetes masters.
2) VPC integrations

Implemented through a CNI Plugin (Open sourced) working on ENIs (automatically attached) . This means that any pod will be seen with a secondary ip (associated to the ENI) in a different subnet from instances subnets. Security group rules will be applied the pods’ ip as any other VPC handling (VPC routing, SG ,ACL) . It will not more required install an overlay network. No info have been given about ALB integration but an integration ECS-like with Kubernetes Services/Target Group is expected (this would be THE ADDED VALUE respect other implementation on AWS)
3) Integration with Private Link Interface

Amazon EKS supports PrivateLink as a method to access your Kubernetes masters and the Amazon EKS service. With PrivateLink, your Kubernetes masters and Amazon EKS service API endpoint appear as an elastic network interface (ENI) with private IP addresses in your Amazon VPC. This allows you to access the Kubernetes masters and the Amazon EKS service directly from within your own Amazon VPC, without using public IP addresses or requiring the traffic to traverse the internet. Again ENI will be subject to any VPC (Acl and Security Group and FLow Logs to/from Masters).
4)Intergration with Cloudtrail and Cloudwatch Logs

Amazon EKS is integrated with Amazon CloudWatch Logs and AWS CloudTrail to provide visibility and audit history tracking of your cluster and user activity. You can use CloudWatch Logs to view logs from your Kubernetes masters, and you can use CloudTrail to view logs on API activity to the Amazon EKS service endpoint.
Personal Considerations

EKS implementation looks like the ECS one (apart the CNI networking which is really the value added ( for micro services architectures) of kubernetes solution towards an ECS one . Kubelet will handle what ecs agent does , in addition there will be the cni plugin again and an IPAM for each node instance. For kubernetes addons will be present at least a kubeDNS implementations (integrated with R53?) and kubectl and ..?

For these reason I’ll come back to analyze ECS solutions and tools..
But the most important thing to note is that AWS is following its “Open Sourced” component as it has done previously with ECS ….( container world is open)


