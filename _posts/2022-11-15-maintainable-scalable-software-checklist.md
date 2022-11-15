---
layout: post
title: "Maintainable and Scalable Software: A Checklist"
date: "2022-11-15"
categories: general
---


![]({{ site.baseurl }}/assets/images/swscale.png)

I think this serves as a good checklist to have when designing/developing software especially if this software is meant to grow as customer base grows.  I also included a definition of what software scalability means plus a list of current technologies that developers use to help tham scale their softwares.

## Software Scalability Definition
Software scalability is a measure of how easy it is to grow or shrink a piece of software. In many cases it refers to the software’s ability to handle increased workloads while adding users and removing them with minimal cost impact. Often software scalability also refers to the software’s ability to perform and support growing amounts of data.

The keys to software scalability include **hardware infrastructure**, **software selection** and **cloud accessibility**


## Checklist
- Make software easy to change, update, or add features later on
    - Product flexibility from day one
- Keep things as simple as possible
    - Apply the K.I.S.S. principle (see [The K.I.S.S Principle in Programming](https://dev.to/kwereutosu/the-k-i-s-s-principle-in-programming-1jfg))
- Keep your code clean and readable
    - Avoid overusing conditional statements
    - Keep variables and functions meaningful and descriptive
    - Use loops
- Create modular components with well-defined interfaces
    - Adopt the S.O.L.I.D. design principles (my post [here](/tech-blog/2017/11/07/dont-confuse-dip-ioc-and-di-together-they-are-all-different-but-related.html) defines what SOLID stands for)
- Adopt continuous integration practices
    - Automate building, testing, and deploying software
    - Test early and test often
    - Include performance and load testing
    - Option for canary or blue/green release strategies
- Make sure data storage solution is scalable
    - Option for multiple and distributed databases but synchronization will be a challenge
- Avoid storage
    - Rely on storage only for the most critical components
- Build stateless applications
    - Make sure application does not store any session data to use in another session
- Use asynchronous communication
    - Synchronous or serial tasks are a big bottleneck on scale
    - Run tasks in parallel
- Queue automation tasks
    - Avoid waiting on long running tasks by queueing them and get notified when done
- Use read replicas
    - Reduce load on primary DB by routing read queries from applications to the read replica
- Reduce write requests
    - Controlling or buffering write operations
- Scale servers appropriately
    - Scaling vertically (up/down) which means adding more servers as opposed to scaling horizontally which means adding more resources to one server
    - Decide based on application traffic how conservative or aggressive it needs to scale
- Use a robust caching engine and a good CDN provider
    - Multi-location caching
    - Edge computing platform
- Add observability (e.g. logging, monitoring and alerting) to operate at scale


## Technologies
Microservices, CQRS, event sourcing, ECS, Kubernetes, elastic storage, CDNs, load balancers, data lakes, Docker, Go, GraphQL, Snowflake, BigQuery, AWS elastic containers with auto-scaling, AWS DynamoDB, S3, Apache Zookeeper, Kafka, Apache Spark, AWS EMR, AWS Athena, Redshift, GCP autoscaling, Elixir, ZenMonitor, Manifold, Semaphore, ScyllaDB, Rust, Ansible, Terraform, JMeter and queries, BlazeMeter, Grafana dashboards, New Relic, Cassandra, Cloudfront, Elastic Beanstalk, Fargate, Sumo Logic, Datadog, Google's Firebase toolset, Azure App Service, Azure SQL, Azure Cache for Redis, Promotheus, RDS, Thanos, ESLint, RuboCop, AWS Lambda, GitFlow, Docker Compose, AWS CodeBuild, Logz.io, gRPC, Airflow


## References
- [How to Design Maintainable and Scalable software](https://www.adservio.fr/post/how-to-design-maintainable-and-scalable-software#el4)
- [How To Design Scalable Applications In 10 Steps](https://www.snapt.net/blog/how-to-design-scalable-applications-in-10-steps)
- [WHAT IS SOFTWARE SCALABILITY AND WHY IS IT IMPORTANT?](https://www.cyberlinkasp.com/insights/what-is-software-scalability-and-why-is-it-important/)
- [What Is Scalability and How Do You Build for It? 25 Engineers Weigh In](https://builtin.com/software-engineering-perspectives/what-is-scalability)

