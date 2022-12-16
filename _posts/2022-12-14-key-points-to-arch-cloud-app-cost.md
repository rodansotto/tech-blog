---
title: "Key Points To Architecturing Cloud Applications, Part 1: Cost"
date: "2022-12-14"
categories: 
  - "cloud"
---


![]({{ site.baseurl }}/assets/images/cloud-cost.png)


These are key points from the course I took recently on [Build great solutions with the Microsoft Azure Well-Architected Framework](https://learn.microsoft.com/en-us/training/paths/azure-well-architected-framework/).  I think these points are applicable no matter which cloud provider you use.  This will be a 5-part series on cost, operations, performance, reliability and security considerations on architecturing cloud applications.

Here are the links to the other parts:
- [Part 2: Operations](/tech-blog/2022/12/16/key-points-to-arch-cloud-app-ops.html)

<p></p>
This is Part 1: Cost and below are the key points to optimize cost for your cloud architecture.


## Plan and estimate your cloud costs

Like which services to select, which service tier or virtual machine (VM) size to choose, do you provision VMs for your workload?, or take advantage of higher-level (application) services that can reduce operational costs (e.g. Azure Functions/AWS Lambda/GCP Cloud Functions)

- Make sure to capture business and technical requirements

- Use pricing calculator from the cloud provider

- Include future investments since no architecture is static

- Organize resources into resource groups to enable control, reporting, and attribution of costs throughout your environment, e.g. to report on usage by product, business unit, or project

- Budget for education to ensure your staff is properly trained to build and maintain resource on cloud


## Provision with optimization

### Select appropriate service tiers and sizes

- Carefully evaluate workload/resource requirements for your application

- How much CPU, memory and storage is required

### Pay only for consumption

- Pay for only the amount of transactions, CPU time, or run time of your application

### Use spot instances for low-priority workloads

- Take advantage of unused capacity on the cloud provider at a significant cost savings

- Best for batch processing jobs and the like

### Use managed services when possible

- This avoids managing the underlying infrastructure or lower-level services

- Managed services are the application and database services


## Take advantage of reserved instances

- Committing yourself to 1 year or multi-year plans on multiple products instead of going for pay-for-what-you-use cost model might save you more

- Best for consistent resource usage


## Use monitoring and analytics to gain cost insights

This ensures costs aren't growing out of control and detects areas to improve efficiency.  Resource demands will shift over time and cloud services will evolve.

### Track your cloud spend

- Track where your costs are going and how they're allocated across your resources

### Conduct cost reviews

- Regularly check your costs to track your cloud spending

### Respond to cost alerts

- Configure alerts that are based on spending, such as alerts on budget or department spending quota

### Report anomalies

- Active engagement on cost can ensure that you identify a potential for cost overrun before it becomes problematic


## Maximize efficiency of cloud spend

By determining whether the increase is the result of natural, efficient growth, or whether the cost can be reduced by improving efficiency with the organization's cloud resources.  But make sure maximizing efficiency doesn't negatively affect the performance of your system (e.g. running a system at 100% utilization runs the risk of introducing performance issues)

### Optimize IaaS costs

- Compute

  - Choose a smaller size for the virtual machine instance

  - Reduce the number of hours a virtual machine runs (e.g. implementing shutdown schedules)

  - Use discounts for the compute costs if available

<p></p>
- VM disk storage

  - If performance is not required, go for a standard storage instead

### Optimize PaaS costs

- Optimize database costs

  - Single database server vs elastic pool of databases

  - Using elastic pool makes sense for multiple databases that have unpredictable bursts or spikes in activity because database transaction units (DTUs) or virtual cores (vCores) are shared among the databases in the pool, in essence you are provisioning resources for the entire pool

<p></p>
- Optimize blob storage costs

  - Blob storage is a good place to store all your unstructured data that can be accessed in massive scale

  - Take advantage of discounts based on access tier if available: does your data need to be accessed often, infrequently or rarely and explore options to move data from temporary storage to a more permanent storage

<p></p>
- Consumption pricing models

  - Moving to pay-for-what-you-use model can save you money

  - Services like Azure Functions/AWS Lambda/GCP Cloud Functions are billed on number of executions, length of execution time, and the amount of memory used


## Links to architecture from Azure, AWS, and Google Cloud
- [Microsoft Azure Well-Architected Framework](https://learn.microsoft.com/en-us/azure/architecture/framework/)
- [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected)
- [Google Cloud Architecture Framework](https://cloud.google.com/architecture/framework)
