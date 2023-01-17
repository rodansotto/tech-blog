---
title: "Key Points To Architecturing Cloud Applications, Part 2: Operations"
date: "2022-12-16"
categories: 
  - "cloud"
---


![]({{ site.baseurl }}/assets/images/cloud-ops.png)


These are key points from the course I took recently on [Build great solutions with the Microsoft Azure Well-Architected Framework](https://learn.microsoft.com/en-us/training/paths/azure-well-architected-framework/).  I think these points are applicable no matter which cloud provider you use.  This will be a 5-part series on cost, operations, performance, reliability and security considerations in architecturing cloud applications.

Here are the links to the other parts:
- [Part 1: Cost](/tech-blog/2022/12/14/key-points-to-arch-cloud-app-cost.html)
- [Part 3: Performance](/tech-blog/2023/01/16/key-points-to-arch-cloud-app-perf.html)

<p></p>
This is Part 2: Operations and below are the key points to ensure smooth operations for your cloud architecture.


## Design, build, and orchestrate with modern practices

### DevOps
    
- Bring development and operation functions together and break down the existing barriers between them in the goal of providing continuous delivery of value to end users

- Use modern agile tools like Kanban boards, backlogs, dashboards, and scrum boards to help your team get greater visibility into the work that's planned and work that's been delivered

- Use a version-control platform like GitHub that allows a global community of individuals and teams to collaborate on software-development projects

- Be able to build and test deployments, track issues, and create custom workflows in repositories, like in Github

### Continuous Integration and Continuous Delivery (CI/CD)

- Continuous Integration (CI) is the practice of building and testing code every time a team member commits changes to version control

- CI helps developers to identify bugs earlier, and it improves software quality since code is checked in, built, and verified more frequently

- Continuous Delivery (CD) is the process to build, test, configure and deploy from a build environment to a production environment

- Continuous integration and continuous delivery are often combined into a single pipeline known as CI/CD

- CI/CD moves code from development to testing to production and should be automated

- Use tools like GitHub Actions to build workflows that are custom automated processes to build, test, package, release, and deploy code

### Microservices

- Employing microservices architecture that consists of services that are small, independent, and loosely coupled

- You can deploy and scale each service independently

- Because each service is independent, services can use different technology stacks, frameworks, and SDKs

- It's common to see services rely on REST calls for service-to-service communication by using well-defined APIs

### Environment consistency

- A key piece of ensuring that you can develop and deploy applications with confidence is making sure that your environments are consistent between development, test, and production

- Including your environment definitions as part of your deployment will help ensure that your code is built and deployed on a consistent, end-to-end infrastructure


## Use monitoring and analytics to gain operational insights

Monitoring is the act of collecting and analyzing data to determine the performance, health, and availability of your business applications and the resources on which they depend.

### Activity logging

- Collect detailed information about what's happening with your cloud resources, such as:

    - Who attached a disk to this virtual machine?
    - When was this machine shut down?
    - Who changed the load balancer configuration?
    - Why did the autoscale operation on my Virtual Machine Scale Set fail?

<p></p>
- Usually retained for a set period of time but should include option to archive or send to another sink for longer retention and further analysis

### Health of cloud services

- Use a health tool to identify any issues with cloud core services that might affect your application

### Metrics and diagnostics

- Use diagnostics to troubleshoot issues

- Use metrics to provide performance statistics for different resources, and even the operating system inside a virtual machine

- create alerts based on these diagnostics and metrics

### Recommendations on best practices

- If available, take advantage of a tool that provides guidance and recommendations that would result in greater availability, reduced cost, or improved security on your cloud resources

### Infrastructure and application monitoring
    
- When you're designing a monitoring strategy, it's important to include every component in the application chain so you can correlate events across services and resources

- Pull log/analytics information from database server

- Configure services to send log/analytics

- Install agents on VMs to send log/analytics

- Implement or install an instrumentation package into your application  

- Send these data to a centralized logging/analytics tool


## Use automation to reduce effort and error

Using automation to manage the infrastructure ensures that each system is configured properly, with no variance between systems

### Infrastructure as code

- Infrastructure as code (IaC) is the management of infrastructure (such as networks, virtual machines, load balancers, and connection topology) in a descriptive model, using a versioning system that's similar to what's used for source code

- IaC is a key DevOps practice, and it's often used in conjunction with continuous delivery

- Imperative automation

    - Automating infrastructure through a scripting language or SDK usually done via command line interface (CLI) or a scripting shell

<p></p>
- Declarative automation

    - Automating infrastructure through the use of template files, JSON-structured files being the commonly used files

### VM images vs. post-deployment configuration

- For many virtual machine deployments, likely there's additional configuration that you need to take care of before the VM can actually serve its intended purpose, e.g. installation and configuration of the actual workload

- There are two common strategies that you can use for the configuration work

    - Custom images

        - Working with custom images can speed up your overall deployment time, because as soon as the virtual machine is deployed and running, no additional configuration would be needed

        - But you'll need to ensure there's a process to handle image updates, security patches, and inventory management of the images themselves

    <p></p>
    - Post-deployment scripting

        - Leverages a basic base image, then relies on scripting or a configuration-management platform to perform the necessary configuration after the VM is deployed

        - But build times can be extended that can impact how quickly you can scale your VMs

### Automation of operational tasks

- Once your solutions are up and running, there are ongoing operational activities that you can also automate, such as:

    - Periodically searching for orphaned disks
    
    - Installing the latest security patches on VMs
    
    - Searching for and shutting down virtual machines in off hours
    
    - Running daily reports and producing a dashboard to report to senior management

### Automate development environments

- Using automation to deploy VMs with all of the correct tools and repositories that your developers need


## Testing strategies for your application

If automation gives DevOps the required speed and agility to deploy software quickly, only through extensive testing will those deployments achieve the required reliability that customers demand.

Testing should occur on both application code and infrastructure code, and they should both be subject to the same quality controls.

### Automated Testing

- Unit Testing

    - Unit tests are tests typically run by each new version of code that's committed into your version-control system

<p></p>
- Smoke Testing

    - Smoke tests are more exhaustive than unit tests, but still not as much as integration tests

    - They verify that each component can be correctly built, and each component meets your criteria for expected functionality and performance

<p></p>
- Integration Testing

    - Integration testing determines whether your components can interact with each other as they should

    - They usually take longer than smoke testing, and consequently they're sometimes executed less frequently

### Manual Testing

- Acceptance Testing

    - Blue/Green deployments

        - When deploying a new application version, you can deploy it in parallel to the existing one

    <p></p>
    - Canary releases

        - In this scenario, we're talking about releasing functionality (via feature flags), and not necessarily about deploying a new version of the application

    <p></p>
    - A/B testing

        - Similar to canary release testing, but while canary releases focus on mitigating risk, A/B testing focuses on evaluating the effectiveness of two versions of a functionality

    <p></p>
    - Consider collecting data on how your users are using your application

<p></p>
- Stress tests

    - Test whether your application and infrastructure code will both be able to adapt to changing load conditions

    - It's critical that you monitor all the components of the system in order to identify whether there are any scale limitations

<p></p>
- Fault injection

    - Introducing faults in the underlying infrastructure and observing how your application behaves is fundamental for increasing the trust in your redundancy mechanisms, making it resilient to infrastructure failures

    - Can use automated frameworks for this or use a more controlled manual way

    - Possibly adopt chaos engineering where you purposefully make key pieces of infrastructure unavailable

<p></p>
- Security tests

    - Routinely test your application for security vulnerabilities

    - Can include automated security scans

    - Can also include red team exercises, where security teams attempt to compromise your application
