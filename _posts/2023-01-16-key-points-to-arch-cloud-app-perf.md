---
title: "Key Points To Architecturing Cloud Applications, Part 3: Performance"
date: "2023-01-16"
categories: 
  - "cloud"
---


![]({{ site.baseurl }}/assets/images/cloud-perf.png)


These are key points from the course I took recently on [Build great solutions with the Microsoft Azure Well-Architected Framework](https://learn.microsoft.com/en-us/training/paths/azure-well-architected-framework/).  I think these points are applicable no matter which cloud provider you use.  This will be a 5-part series on cost, operations, performance, reliability and security considerations in architecturing cloud applications.

Here are the links to the other parts:
- [Part 1: Cost](/tech-blog/2022/12/14/key-points-to-arch-cloud-app-cost.html)
- [Part 2: Operations](/tech-blog/2022/12/16/key-points-to-arch-cloud-app-ops.html)
- [Part 4: Reliability](/tech-blog/2023/01/30/key-points-to-arch-cloud-app-reliab.html)

<p></p>
**This is Part 3: Performance** and below are the key points to ensure your cloud architecture is performing at its best thus providing users with the best experience.



## Use scaling up and scaling out in your architecture

Scaling resources allows your application to meet demands in times of increased load and provides you cost savings during off peak times.  Scaling in the cloud is usually easier than scaling on-premises and this is one of those main reasons of moving into the cloud.


### Scaling up or down

- When scaling resources for a single instance of a service, such as a virtual machine, you scale up or down

- You increase or decrease the number of resources in a service, such as the cpu capacity, memory capacity, or storage capacity

- Example of a cloud service that can be scaled up or down would be a virtual machine, a database service (to increase/decrease database transaction units for example), or an application service.


### Scaling out or in

- With scaling out and in, the number of instances are adjusted

- In the infrastructure layer, you can increase and decrease the number of VM instances

- In a database, you can employ a sharding technique that splits a large database into multiple smaller database and deployed across multiple servers

- In an application service, if setup in an application farm, you can increase and decrease the number of VMs in the farm.


### Autoscaling

If available, autoscaling allows you to scale your services automatically based on specific metrics like CPU utilization or queue length or schedule.


### Considerations when scaling

- Startup time of your application can impact how quickly your application can scale

  - You might want to add a lead time when scaling

<p></p>
- How your application handles state

  - If an instance is removed the state stored there is lost

  - If an instance is added the state from another instance does not have its state

  - Best to externalize the state to another service such as Redis or a database


### Throttling

- Sometimes the load on an application is caused by the number of active or concurrent users and the activities being performed

- Throttling limits the number of requests from a source and this is one way to prevent the application from breaking

- Used most frequently in applications that expose API endpoints


### Serverless

- Serverless computing provides a cloud-hosted execution environment that runs your apps/code, but completely abstracts the underlying environment

- You configure your serverless apps to respond to events

- Infrastructure isn't your responsibility

- Scaling and performance are handled automatically

- Example of serverless computing is the Azure Functions/AWS Lambda/GCP Cloud Functions


### Containers

- A container is a method of running applications in a virtualized environment at the OS level

- Containers are lightweight and well suited to scale-out scenarios

- They're designed to be created, scaled out, and stopped dynamically as your environment and demands change

- With containers, you don't necessarily need to separate VMs for separate workloads

- Some services that ease the management and scaling of containers

  - Kubernetes Service

  - Cloud specific container management service



## Optimize network performance


### Network latency

- Network latency is the time that it takes for data to travel between a source to a destination across a network

- To improve network performance, we must strive to reduce network latency


### Latency between cloud resources

- Create read-replica of databases in different regions

- Sync your data between regions

- Use a globally distributed database

- Use a caching technology such as Redis


### Latency between users and cloud resources

- Use a DNS load balancer for endpoint path optimization

  - Can distribute traffic within and across regions
  
  - Can route users based on a set of criteria:
    - Priority
    - Weighted
    - Performance (based on network latency)
    - Geographic

<p></p>
- Use a CDN to cache content close to users

  - Using a content delivery network (CDN) can deliver static content such as website pages or image and video assets to users faster

  - You can use CDN to host cached dynamic content but you will need to manage content expiration by setting a time to live (TTL)

- Use a connectivity service from on-premises to cloud provider

  - Optimizing network connectivity from your on-premises environment to cloud is also important

  - Internet connection or even site-to-site VPN over the internet might have an impact on network latency for high-throughput architecture

  - A private dedicated connection between your network and the cloud can give a guaranteed performance



## Optimize storage performance


### Optimize virtual machine storage performance

- Some disk options that your cloud provider might provide:

  - Local SSD storage that is included in VM and is local, thus has a high performance but could be lost during maintenance event or a redeployment of the VM

  - Standard storage HDD that is only HDD and only good for dev/test workload

  - Standard storage SSD that has a low latency of an SSD but only good enough for non production use

  - Premium storage SSD that is well suited for those workloads that are going into production

- Another way to optimize storage performance is to use a striping technology that spreads disk activity across multiple disks; often seen in high-performance database systems


### Optimize storage performance for your application

- Caching

  - Integrate a caching layer between your application and your data store

<p></p>
- Polyglot persistence

  - Use different data storage technologies such as blob store for your application assets, NoSQL store for user related or created data, and a SQL database for your account data (for example)

  - With polyglot persistence, maintaining data consistency can be a significant challenge

  - A more relaxed approach to consistency is used and is known as eventual consistency

  - Eventual consistency means that replica data stores eventually converge if there are no further writes



## Identify performance bottlenecks in your application


### Performance requirements

  - Without performance requirements defined, you could keep improving further and further without end to the point that it becomes prohibitively expensive, difficult, and doesn't have enough business impact to be worthwhile

  - Nonfunctional requirements help you find that point; doesn't tell you what your app must do but tell you what quality levels it must meet

  - You should discuss requirements with your stakeholders or customers, document them, and communicate them broadly to ensure that everyone agrees on what good performance means


### Performance monitoring options in the cloud

- Infrastructure-level logging and monitoring service that can collect following data:

  - Application monitoring data, which is the data about the performance and functionality of the code you've written

  - Guest OS monitoring data

  - Resource monitoring data, which is the data about the operation of a cloud resource

  - Subscription monitoring data (if available)

  - Tenant monitoring data (if available)

<p></p>
- Log analytics tool

  - Centralized logging

  - You can query and aggregate data across logs

<p></p>
- Application performance management

  - Using an APM solution to gain a deep understanding of your application and to correlate activity across your application
