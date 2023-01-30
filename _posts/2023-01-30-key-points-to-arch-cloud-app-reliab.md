---
title: "Key Points To Architecturing Cloud Applications, Part 4: Reliability"
date: "2023-01-30"
categories: 
  - "cloud"
---


![]({{ site.baseurl }}/assets/images/cloud-reliab.png)


These are key points from the course I took recently on [Build great solutions with the Microsoft Azure Well-Architected Framework](https://learn.microsoft.com/en-us/training/paths/azure-well-architected-framework/).  I think these points are applicable no matter which cloud provider you use.  This will be a 5-part series on cost, operations, performance, reliability and security considerations in architecturing cloud applications.

Here are the links to the other parts:
- [Part 1: Cost](/tech-blog/2022/12/14/key-points-to-arch-cloud-app-cost.html)
- [Part 2: Operations](/tech-blog/2022/12/16/key-points-to-arch-cloud-app-ops.html)
- [Part 3: Performance](/tech-blog/2023/01/16/key-points-to-arch-cloud-app-perf.html)

<p></p>
**This is Part 4: Reliability** and below are the key points to ensure a highly available cloud architecture.



## Build a highly available architecture

High availability (HA) ensures your architecture can handle failures.  This availability is often defined by business requirements, service-level objectives, or service-level agreements.


### Evaluate high availability for your architecture

- Determine the service-level agreement of your application
  
  - A service-level agreement (SLA) is an agreement between a service provider and a service consumer, in which the service provider commits to a standard of service based on measurable metrics and defined responsibilities
  
  - Service-level objectives (SLO) are the values of target metrics that are used to measure performance, reliability, or availability, e.g.:
    - Performance of request processing in milliseconds
    - Availability of services in minutes per month
    - Number of requests processed per hour

  <p></p>
  - Identifying SLAs is an important first step when determining the high-availability capabilities that your architecture will require as these will help shape the methods you'll use to make your application highly available

<p></p>
- Evaluate the HA capabilities of the application

  - Perform failure analysis

  - Focus on single points of failure and critical component

  - Evaluate all components including those that provide HA functionalities such as load balancers

  - Determine application's capability to detect error conditions and to self-heal

<p></p>
- Evaluate the HA capabilities of dependent applications

  - You'll also need to understand the provided SLAs of any resource on which your application may depend

  - Dependencies with SLA lower than yours could put you at risk

  - Find ways to meet your SLA while the dependency is unavailable, such as caches and queues


### High availability cloud services

- Availability sets

  - Allows VMs that belong to the same application workload to be distributed to prevent simultaneous impact from hardware failure and scheduled maintenance

  - Made up of update domains and fault domains

    - With update domains, you have some servers/VMs (not all) on one rack that remains running during maintenance
    - With fault domains, you have more than 1 rack available such that an outage in one rack will not affect the other racks

<p></p>
- Availability zones

  - With availability zones, you have more than 1 physical datacenter location within a region available for you so you can protect yourself from datacenter outages while retaining presence in a particular region

  - Mutually exclusive with availability sets as you no longer need to define an availability set for your systems

  - You'll have diversity at the data-center level, and updates will never be performed to multiple availability zones at the same time


- Load balancing

  - Load balancers manage how network traffic is distributed across an application

  - For applications that don't have service discovery built in, load balancing is required for both availability sets and availability zones

  - Types of load balancing:

    - DNS load balancing
      - Directs users to multiple IP addresses (server machines) for a single domain
      - DNS returns a list of all the servers' IP addresses in response to a name resolution request

    <p></p>
    - Layer 7 (Application layer) load balancing, such as an application gateway
      - Provides distribution (e.g. round-robin) of incoming traffic, cookie-based session affinity, URL path-based routing

    <p></p>
    - Layer 4 (Transport layer) load balancing
      - Provides distribution at the transport layer by using only the TCP and HTTP health-probing options
      - No smart load balancing because the load balancer can't access request content


<p></p>
- Platform as a service (PaaS) HA capabilities

  - Usually comes with high availability built in

  - Using PaaS services is one of the best ways to ensure that your architecture is highly available



## Develop a disaster recovery strategy

Disaster recovery is about recovering from high-impact events that result in downtime and data loss.  And the best remedy for a disaster once it has occurred is a well-defined, tested disaster recovery plan and an application that actively supports disaster recovery efforts through its design.


### Create a disaster recovery plan

A disaster recovery plan is a single document that details the procedures that are required to recover from data loss and downtime caused by a disaster and identifies who's in charge of directing those procedures.

- Risk assessment and process inventory

  - The first step in creating a disaster recovery plan is performing a risk analysis that examines the impact of different kinds of disasters on the application

  - The risk assessment needs to consider every process that can't afford unlimited downtime, and every category of data that can't afford unlimited loss

<p></p>
- Recovery objectives

  - A complete plan needs to specify two critical business requirements for each process implemented by the application:

    - Recovery Point Objective (RPO)

      - The maximum duration of acceptable data loss

      - Measured in units of time, not volume: "30 minutes of data", "four hours of data", and so on

      - Is about limiting and recovering from data loss

    - Recovery Time Objective (RTO)

      - The maximum duration of acceptable downtime

  <p></p>
  - Each major process or workload that's implemented by an app should have separate RPO and RTO values

  - The process of specifying an RPO and RTO is effectively the creation of disaster recovery requirements for your application

<p></p>
- Detailing recovery steps

  - The final plan should go into detail about exactly what steps should be taken to restore lost data and application connectivity. Steps often include information about:

    - Backups: How often they're created, where they're located, and how to restore data from them
    
    - Data replicas: The number and locations of replicas, the nature and consistency characteristics of the replicated data, and how to switch over to a different replica
    
    - Deployments: How deployments are executed, how rollbacks occur, and failure scenarios for deployments
    
    - Infrastructure: On-premises and cloud resources, network infrastructure, and hardware inventory
    
    - Dependencies: External services that are used by the application, including SLAs and contact information
    
    - Configuration and notification: Flags or options that can be set to gracefully degrade the application, and services that are used to notify users of application impact


### Design for disaster recovery

Disaster recovery is not an automatic feature. It must be designed, built, and tested.  Designing for disaster recovery has two main concerns:

- Data recovery and replication

  - Unlike backup, which creates long-lived, read-only snapshots of data for use in recovery, replication creates real-time or near-real-time copies of live data

  - Replication is used to mitigate a failed or unreachable data store by executing a failover: changing application configuration to route data requests to a working replica

  - Most fully featured database systems and other data-storage products and services include some kind of replication as a tightly integrated feature due to its functional and performance requirements

  - Many different replication designs exist that place different priorities on data consistency, performance, and cost:

    - Active replication requires updates to take place on multiple replicas simultaneously, guaranteeing consistency at the cost of throughput

    - Passive replication performs synchronization in the background, removing replication as a constraint on application performance, but increasing RPO

    - Active-active or multi-master replication enables multiple replicas to be used simultaneously, enabling load balancing at the cost of complicating data consistency

    - Active-passive replication reserves replicas for live use only during failover

- Process recovery

  - After a disaster, business data isn't the only asset that needs recovering

  - Process restoration involves failover to a separate, working deployment of your application


### Test a disaster recovery plan

  - Testing the plan is a crucial aspect of disaster recovery to ensure that the directions and explanations are clear and up to date

  - Choose intervals to perform different types and scopes of tests, such as testing backups and failover mechanisms every month, and performing a full-scale disaster recovery simulation every six months

  - Make sure to include your monitoring system in your testing as well



## Protect your data with backup and restore

Backup is the final and most powerful line of defense against permanent data loss.


### Establish backup and restoration requirements

To establish backup requirements for your app, group your application's data based on the following requirements:

  - How much of this type of data can afford to be lost, measured in duration

  - The maximum amount of time a restore of this type of data should require

  - Backup retention requirements: how long and at what frequency do backups need to remain available

  - Don't confuse archival as archival is the storage of data for long-term preservation and read access


### Cloud backup and restore capabilities

  - General-purpose backup solution for cloud and on-premises workflows that run on VMs or physical servers

  - Blob storage backup

  - Automatic database backup

  - App service scheduled and manual backup


### Verify backups and test restore procedures

  - By creating a new deployment of the application, restoring the backup to it, and comparing the state of the two instances

  - Simply performing a comparison of a subset of the backup data with the live data immediately after creating a backup can be enough
