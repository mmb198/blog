---
title: "Cloud Engineer Academy Week 2 Blog"
date: 2024-02-21T21:37:43+08:00
toc: false
images:
tags: 
  - cloudengineeringacademy
  - week2
---

# Version Control
Learnt about 3 main types of version control systems:
	1. Local: All repositories/data are only held and accessible from a local machine, making it difficult to collaborate with others. 
	2. Centralised: The repository is kept on a main server, any updates have to be committed to the central server.
	3. Distributed: Repositories are distributed across end users and servers. Any of the users or servers can act as the central repository. 
# GIT
-  Set up a GitHub account, configured MFA and ssh access. Command to check that ssh is connected **ssh -T git@github.com
- Installed git in Windows and Linux and set up CLI access via ssh. 
	- SSH encrypts the data flow between my machine and github, ensuring confidentiality in the transmission of data that I commit to the repo.
# AWS CLI
- Installed the AWS CLI in Windows and Linux
 - Added security keys in AWS console and installed them into AWS CLI. This now enables control of my AWS account through the CLI. The CLI is definitely faster than clicking and confirming through the console.
 - Command structure:
aws + service type + what you want to do, examples:
aws + s3 service + list files = **aws s3 ls**
aws + iam + list access keys = **aws iam list-access-keys**

# Cloud Architecture & System Design
## Front end vs back end
- Front end = user facing, interacts with the backend via API's (Application Programming Interface).
- Back end = All of the infrastructure and applications that enables the front end to function.
## Vertical vs Horizontal scaling
- Vertical scaling = increasing or decreasing the size of the hardware - such as EC2 t2.micro, t2.small, t2.medium etc. As the size increases additional hardware is provided such as more CPU cores and memory.
- Horizontal scaling = Instead of increasing hardware capacity as with vertical scaling, horizontal scaling instead increases the amount of instances. Instead of increasing from a t2.micro instance to a single t2.small instance, you could run 3 x t2.micro instances. This provides additional computing resources and also provides redundancy as there are now two extra compute instances in the event that one of them becomes unresponsive or crashes.  
## Load Balancing
These can be hardware or software that distributes data across your infrastructure. Is used to ensure that a server isn't being overloaded while other servers are sitting idle. Can also decide which server is closest to the end user in order to reduce latency for their request.
## High Availability and Fault Tolerance
- High availability = Redundancy within a network that enables standby infrastructure to take over in the event of the main services becoming unresponsive or crashing. Multiple instances can be used across different Availability Zones (AZ) to ensure continued operation even if an AZ experiences an outage. Use of health checks, auto scaling and load balancing to maintain high availability.
- Fault tolerance = The ability to continue providing services in the event of a fault, issue or outage. Intent is that faults do not impact the user experience.
## Lab - Design a Web Application Architecture

![AWS web app architecture v3](/week2.png)

Summary of Cloud Architecture for Web Application

This document outlines the purpose of each component and the rationale behind key architectural decisions in our cloud architecture for the web application.

**Components:**

- **VPC (Virtual Private Cloud):** Provides a secure and isolated environment for our application resources.
- **Route 53:** Routes incoming traffic to the application through a domain name.
- **Public and Private Subnets:** 
- **Public Subnets:**
    - **Purpose:** Host web servers that require internet access to serve content to users.
    - **Reasoning:** Enables users to access the application through the internet.
- **Private Subnets:**
    - **Purpose:** Host application servers and databases that don't require direct internet access but need to communicate with web servers.
    - **Reasoning:** Enhances security by restricting access to critical components from the public internet.
- **Web Servers and Application Servers:** 
- **Web Servers (EC2 Instances):**
    - **Purpose:** Serve static content (HTML, CSS, JavaScript) and handle initial user requests.
    - **Reasoning:** Offloads static content serving from application servers, improving performance and scalability.
- **Application Servers (EC2 Instances):**
    - **Purpose:** Process application logic, interact with the database, and generate dynamic content.
    - **Reasoning:** Provides flexibility and scalability for handling application logic and database interactions.EC2 instances host the web application and application logic.
- **Load Balancers:** 
	- **Purpose:** Distribute incoming traffic evenly across multiple web and application servers.
	- **Reasoning:** Ensures high availability and prevents overloading individual servers, improving application performance and scalability.
- **AWS WAF:** Protects the web application from malicious attacks.
	- - **Purpose:** Filters and blocks malicious traffic attempting to exploit vulnerabilities in the web application.
	- **Reasoning:** Strengthens application security by mitigating common web attacks like SQL injection and cross-site scripting
- **Amazon RDS (Relational Database Service):** 
	- **Purpose:** Provides a managed, scalable, and highly available database service for storing application data.
	- **Reasoning:** Offers a reliable and secure solution for managing application data without the need for manual database administration.
- **AWS S3:** 
	- - **Purpose:** Stores static content like images, videos, and other application assets cost-effectively and efficiently.
	- **Reasoning:** Provides a scalable and cost-effective way to store and manage large amounts of static content, offloading storage from web servers and improving performance.


**Architectural Decisions:**
- **Horizontal Scaling:** Web and application servers are deployed in auto scaling groups for horizontal scaling. This allows automatic scaling up or down based on traffic demands, ensuring optimal performance and resource utilization.
- **Redundancy:** Deploying critical components like web servers, application servers, and databases across multiple availability zones within the VPC ensures continued operation even if one zone experiences an outage.
- **Security:** Utilizing a VPC with public/private subnets and a WAF strengthens the application's security posture by isolating resources and filtering malicious traffic.