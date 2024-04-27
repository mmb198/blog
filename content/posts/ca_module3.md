---
title: "Cloud Engineer Academy Module 3 Blog - System Design and Architecture"
date: 2024-04-21T21:32:09+08:00
toc: false
images:
tags: 
  - cloudengineeringacademy
  - module3
---

The Cyber Engineering Academy started as a 12 week course with a new subject per week (12 weeks = 12 subjects) but this was a little ambitious! The reality is that a single week for AWS (week 5), isn't enough time so this timeline has been blown out. I'll now be referring to modules rather than weeks.

Module 3 - System Design and Architecture
This module covered common architecture types (monolithic, microservices and serverless), Application Programmable Interfaces (APIs), Load Balancers and cloud storage options (object, block and file). 

I'm only doing a short summary for the blog as I'm posting the architecture project below and it covers in detail all three architecture types, explains use cases and advantages and disadvantages for architecture type. 

## Part 1: Monolithic Architecture Design

**Core Functionalities:**
1. User registration
2. Product catalog
3. Shopping cart
4. Order processing

**High-Level Architecture Diagram:**

```
|------------------------|
|         Frontend       |
|------------------------|
            |
            v
|------------------------|
|    Business Logic      |
|      (Monolith)        |
|------------------------|
            |
            v
|------------------------|
|        Database        |
|------------------------|
```

**Advantages:**
- **Simplicity and Uniformity:** Easy to develop, deploy, and manage as everything is contained within a single codebase.
- **Ease of Deployment:** Deployment is straightforward as there's only one unit to deploy.

**Disadvantages:**
- **Scalability:** Scaling the application can be challenging as all components are tightly coupled, making it difficult to scale individual parts independently.
- **Flexibility:** Changes or updates to one part of the application may require redeploying the entire monolith.
- **Deployment:** Scaling the monolith horizontally can be costly and inefficient.

## Part 2: Refactoring into Microservices

**Identified Microservices:**
1. User Service
2. Product Service
3. Cart Service
4. Order Service

**Updated Architecture Diagram:**

```
|------------------------|
|         Frontend       |
|------------------------|
            |
            v
|------------------------|
|     User Service       |
|------------------------|
            |
            v
|------------------------|
|    Product Service     |
|------------------------|
            |
            v
|------------------------|
|     Cart Service       |
|------------------------|
            |
            v
|------------------------|
|    Order Service       |
|------------------------|
            |
            v
|------------------------|
|     Database(s)        |
|------------------------|
```

**Advantages:**
- **Scalability:** Each microservice can be scaled independently based on demand, allowing for more efficient resource utilisation.
- **Flexibility:** Changes or updates to one microservice can be made without affecting others, enabling faster development and deployment.
- **Deployment:** Each microservice can be deployed independently, facilitating Continuous Deployment/Continuous Integration (CI/CD) practices.

**Challenges:**
- **Development Complexity:** Managing multiple services can increase development complexity, especially in terms of communication between services.
- **Deployment:** Coordinating deployments across multiple services requires careful orchestration to maintain consistency and avoid service disruptions.
- **Consistency:** Ensuring consistency in data management and transactions across distributed services can be challenging.

## Part 3: Incorporating Serverless Architecture

**Identified Serverless Components:**
1. User Authentication
2. Payment Processing

**Updated Architecture Diagram:**

```
|------------------------|
|         Frontend       |
|------------------------|
             |
             v
|------------------------|
|    User Authentication |  (Serverless)
|------------------------|
             |
             v
|------------------------|
|   Product & Order APIs |  (Microservices)
|------------------------|
             |
             v
|------------------------|
|   Payment Processing   |  (Serverless)
|------------------------|
             |
             v
|------------------------|
|     Database(s)        |
|------------------------|
```

**Benefits of Serverless Architecture:**
- **Scalability:** Serverless functions auto-scale based on demand, ensuring resources are efficiently utilised and reducing the risk of over-provisioning.
- **Cost:** Serverless architectures offer cost savings as you only pay for the resources consumed during execution, rather than provisioning fixed resources.
- **Operational Management:** Serverless providers handle server management, scaling, and maintenance, reducing operational overhead for the development team.

**Challenges:**
- **Cold Start:** Serverless functions may experience latency during cold starts, impacting the responsiveness of the application.
- **Vendor Lock-in:** Adopting serverless architectures may lead to vendor lock-in due to reliance on specific cloud providers' services and APIs.
- **Debugging and Monitoring:** Debugging and monitoring serverless functions can be more challenging compared to traditional architectures.

**Comparison Report:**

1. **Scalability:**
   - Monolithic: Limited scalability due to tight coupling.
   - Microservices: Highly scalable, each service can be scaled independently.
   - Serverless: Autoscaling capabilities offer efficient resource utilisation.

2. **Development Complexity:**
   - Monolithic: Simple development but can become complex as the application grows.
   - Microservices: Increased complexity due to managing multiple services.
   - Serverless: Simplifies development by abstracting infrastructure management, but can be complex in orchestrating functions.

3. **Deployment:**
   - Monolithic: Simple deployment but requires redeployment of the entire application for updates.
   - Microservices: Requires careful orchestration for deployment across multiple services.
   - Serverless: Facilitates easy and rapid deployments of individual functions.

4. **Maintenance:**
   - Monolithic: Maintenance can be cumbersome, especially for large applications.
   - Microservices: Each service needs to be maintained individually.
   - Serverless: Reduces operational overhead as infrastructure management is handled by the provider.

5. **Cost Implications:**
   - Monolithic: Fixed infrastructure costs regardless of usage.
   - Microservices: Costs may vary based on the number of services and their usage.
   - Serverless: Cost-efficient as you only pay for actual usage.

**Suitability for Different Projects:**
- Monolithic: Suitable for small-scale projects with predictable usage.
- Microservices: Ideal for large-scale projects with complex requirements and variable loads.
- Serverless: Well-suited for projects with sporadic or unpredictable workloads and where cost optimisation is crucial.

Each architectural style has its strengths and weaknesses, and the choice depends on the specific requirements, scale, and constraints of the project.