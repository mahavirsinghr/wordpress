# wordpress

**BRIEF:**
A potential customer is looking for help in scaling their platform on the cloud. They are a startup ecommerce company in the early stages of their operations. 

Currently their architecture uses a Wordpress server with a Woocommerce plugin all running on a small shared development server. They have recently created an ad campaign that is generating a lot of traction and expect a lot of growth in the next few months. 

They would like to understand how they could take advantage of the latest cloud technology available and are willing to make large development changes if necessary, but are okay with their current stack. They are not averse to looking at newer containerization technology either. They have a strong development team but don’t have any rigor in place around how they can automate deployments to their infrastructure.

**They would like to know the following:
**
●How can they scale to meet the demand?
●Get the ability to easily manage and replicate multiple environments based on their blueprint architecture. 
●How they should create a CI / CD setup
●They want to have the ability to recover from any Disasters that may impact their website.
●They want to effectively distribute load
●Improve user experience by reducing latency to their end customers
●A self-healing infrastructure that recovers from failures
●Security of data at rest and in transit
●Securing access to the environment
●Ensure their operations team can monitor the environment

**OBJECTIVE **
Recommend a manageable, secure, scalable, high performance, efficient, elastic, highly available, fault tolerant and recoverable architecture that allows the startup to organically grow. 
The architecture should specifically address the requirements/concerns as described above. 

**DELIVERABLES** 
A PDF document no greater than three or four pages in length that clearly and succinctly present an analysis of the companies requirements and the proposed architecture diagram. Clearly state all assumptions made during the design and explicitly state the cloud platform used to deploy the new setup.

![image](https://user-images.githubusercontent.com/13980382/130021070-9002e0d2-d855-42a2-918c-b8aad27685fe.png)

https://lucid.app/lucidchart/invitations/accept/inv_aafbaf96-03b5-4f5e-b918-759b5920d32a By Mahavir

**Manageable:** AWS Managed Services (AMS) helps you operate your AWS infrastructure more efficiently and securely. Leveraging AWS services and a growing library of automations, configurations, and run books, AMS can augment and optimize your operational capabilities in both new and existing AWS environments. Whether customers are just getting started, migrating a data centre, or building optimized solutions in the cloud, ongoing operational excellence is a critical component to success in the cloud

**Secure:** services that help you protect your data, accounts, and workloads from unauthorized access (Subnets, VPC)

**Scalability:** A system’s ability to monitor the user demand and automatically increase or decrease resources. This scalability will be provided by the following AWS Resources: AWS ELB, AWS EC2, AWS S3, AWS RDS.

**High Performance:** AWS provides the most elastic and scalable cloud infrastructure to run your HPC applications. With virtually unlimited capacity, engineers, researchers, and HPC system owners can innovate beyond the limitations of on-premises HPC infrastructure

**Efficient:** efficiency pillar provides an overview of design principles, best practices

**Elastic:** Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers. Amazon EC2’s simple web service interface allows you to obtain and configure capacity with minimal friction. It provides you with complete control of your computing resources and lets you run on Amazon’s proven computing environment.
High Availability: It means that a system can operate without any service disruption or interruption for a long time as well as for a system that has redundant components. (In our case the redundant Infrastructure will be our High Availability — Thanks AWS for making this easier!).

**Fault Tolerant:** is the ability for a system to remain in operation even if some of the components used to build the system fail

**Recoverable Architecture:** how to use AWS Regions as your active sites, creating a multi-Region active/active architecture. Only two Regions are shown, which is common, but more may be used. Each Region hosts a highly available, multi-Availability Zone (AZ) workload stack. 

In each Region, data is replicated live between the data stores and also backed up. This protects against disasters that include data deletion or corruption, since the data backup can be restored to the last known good state.

**Traffic routing**
Each regional stack serves production traffic. How you implement traffic routing determines which Region will receive a given request. Figure shows Amazon Route 53, a highly available and scalable cloud Domain Name System (DNS), used for routing. Route 53 offers multiple routing policies. For example, the geolocation or latency routing policies are good choices for active/active deployments. For geolocation routing, you configure which Region a request goes to based on the origin location of the request. For latency routing, AWS automatically sends requests to the Region that provides the shortest round-trip time.
Distributed Services — Loose Coupling: The art of distributing different components of a system in the same network. We will be doing this to leverage the load of any resource and have dedicated hosts for a service.
AWS Services Explained
**
1.	**Route53****
This service will help us to manage all the upcoming requests (traffic) that our domain will be having. AWS Route53 will also be the DNS Manager, so here we will point our domain registrar to be the manager, and once it has been migrated here, we can add the A records, Cnames, or TXT records and many other more.**
2.	**AWS VPC****
The AWS VPC is a service that allows us to have a private network in which we will allocate our cloud computing resources, meaning nobody has access to it, only ourselves.**
3.	AWS Private Subnet**
The private subnet is the subnet in which we are going to deploy the resources we don’t want outsiders to have access to. In this case, our database will be only accessible by the application.
**4.	AWS Public Subnet**
The public subnet is the subnet in which we are going to deploy the resources we want to make public — like the server for our Website.**
5.	AWS S3**
Amazon Simple Storage Service will be our content storage solution. Here our Wordpress installation(s) will have the content available whenever it scales up or off.
**6.	AWS CloudFront**
CloudFront combined with S3 will help us to spread the content faster to the end users. This way our Wordpress multimedia content will be spread all over AWS CDN Network (Edge Locations) which will be used from our application to reduce the latency. Users will be served by the closest edge location available. So faster content = Faster Site.
**7.	AWS Load Balancer**
Here is the tricky part. The AWS ELB will allow us to distribute the traffic load between our instances available or in use depending on how the auto scaling is set.**
8.	AWS EC2**
Instances or also called “VM’s” this is the service on AWS for acquiring computing power. AWS EC2 will allow us to host our Wordpress site and files we need.
**9.	AWS Autoscaling**
The Magic — here is it! This will be the solution for our highly available and scalable Wordpress site. AWS Autoscaling will take care of always having a minimum quantity of instances available for the public and in case something goes wrong, it will replace the instance with a healthy one, this way our site will always be available.
Autoscaling will also benefit our WordPress by creating instances based on the traffic demand and will help us to save costs while the traffic is low.
**10.	AWS RDS & Multi A-Z**
RDS will be the service in which we will host our Wordpress Database. The service is completely free and fully managed by AWS. So that gives AWS plus since we won’t need to worry about the database management anymore. Also, a useful feature is that RDS instances can have replication between them, that adds even more scalability. Another feature which will provide us high availability is enabling the Multi-Availability Zone (Multi A-Z) feature. Keep an eye on this since the price will is double for the RDS.
**11.	AWS Cloudwatch:** will be our trusted supervisor. Cloudwatch will be in charge of monitoring all the resources in our AWS account. It will keep an eye on the metrics that are predefined or as default by AWS resources, such as CPU usage, Memory usage, Disk IO and Networking.
Let me explain you how this environment will be able to serve millions of page 
views / visitors!
 
**Traffic Flow:** 
Here is how your visitors get to your site — once they hit your domain on their browser their request will pass to the internet, route it to your DNS manager and the DNS manager(Route53) will solve the request to the specified server, the web server then, will serve the application.
Server Caching / Wordpress Caching: Server-side caching or Wordpress-side caching with a plugin or embedded in ah host. Whenever someone visits the website he or she requests the homepage for example; the request is passed to the database to retrieve the homepage information. What caching does, it that it creates a temporary file (I say temporary because you can specify the expiration) so when your request comes, it will check for the files it generates instead of processing the request to the database.

**There are different ways in which we can protect our application and user’s data:**
1.	WordPress Plugins to Back up the Site. (S3)
2.	Disaster Recovery for Infrastructure (Physical).
3.	Backup for Users Data (DB — RDS).
4.	Backup for Application Code.

