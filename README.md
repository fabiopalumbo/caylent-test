

# Amazon Web Services Net Diagram Challenge

Revision 1.0 // October 16, 2019

Please produce a network diagram of an n-tier application on AWS and write a 1/2 to 1-page

text description describing your choices and architecture.

The design should support:



*   variable loads,
*   JS frontend,
*   collection of containerized microservices,
*   a Postgres and Mongo DB tier

Additionally, the diagram should make best use of distributed solutions and architecture.


## Diagram



<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.png "image_tooltip")



## 


## Best practices for business continuity and disaster recovery in Amazon  Elastic Kubernetes Service (EKS)



1. Plan for EKS clusters in multiple regions.
2. Route traffic across multiple clusters by using Load Balancer with geo routing policy.
3. Use geo-replication for your container image registries.
4. Plan for application state across multiple clusters.
5. Replicate storage across multiple regions.

Summary: We will deploy this orchestration with Terraform (IaaC). Due to the requirements, a Serverless approach is not recommended due to the escalation and data layers.

A Solution based in Kubernetes is the best approach in my experience. 

Amazon EKS is deeply integrated with services such as Amazon CloudWatch, Auto Scaling Groups, AWS Identity and Access Management (IAM), and Amazon Virtual Private Cloud (VPC), providing a seamless experience to monitor, scale, and load-balance your applications.  Removing the overhead of Master node maintenance.

Plan



1. An EKS cluster is deployed into a single region. To protect your system from region failure we will deploy the application into multiple EKS clusters across different regions. 
2. Load Balancer can direct customers to their closest EKS cluster and application instance. For the best performance and redundancy, we will direct all application traffic through ALB (Layer 7) before it goes to your EKS cluster.
3. Store your container images in Elastic Container Registry and geo-replicate the registry to each EKS region.
4. We will not store service state inside the container. Instead, use an EFS with PVC claims that supports multiregion replication
5. Plan to migrate storage from the primary region to the backup region with EFS Replication to keep the storage synchronized. (DB)
