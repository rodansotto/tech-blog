---
layout: post
title: "From CloudFormation To Serverless Framework To Cloud Development Kit?"
date: "2022-08-02"
categories: cloud
---

![]({{ site.baseurl }}/assets/images/cloud.png)

### AWS CloudFormation

Had the chance to work on [AWS CloudFormation](https://aws.amazon.com/cloudformation/) in my job.  And I did not like it actually.  Had a hard time reading it honestly.  For those who is not familiar with CloudFormation, it's AWS's way of provisioning infrastructure in the cloud as code.

Coming from a programming background, having to write and understand a CloudFormation script is a steep learning curve for me.  I call it a script because it does behave like a script that you run but instead of running code it creates your cloud infrastructure for you.  AWS actually calls it a **CloudFormation template**.

#### YAML
Below is how a CloudFormation template looks.  It's just a snippet and it's in YAML format.
```yaml
Resources: 
  MyInstance: 
    Type: "AWS::EC2::Instance"
    Properties: 
      ImageId: "ami-0ff8a91507f77f867"
      SecurityGroups: !If [CreateNewSecurityGroup, !Ref NewSecurityGroup, !Ref ExistingSecurityGroup]
  NewSecurityGroup: 
    Type: "AWS::EC2::SecurityGroup"
    Condition: CreateNewSecurityGroup
    Properties: 
      GroupDescription: Enable HTTP access via port 80
      SecurityGroupIngress: 
        - 
          IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
```

#### JSON
You can also write the template in JSON.  Below is a snippet:
```json
  "Resources" : {
    "S3Bucket" : {
      "Type" : "AWS::S3::Bucket",
      "Properties" : {
        "AccessControl" : "PublicRead",
        "WebsiteConfiguration" : {
          "IndexDocument" : "index.html",
          "ErrorDocument" : "error.html"
         }
      },
      "DeletionPolicy" : "Retain"
    }
  },
```

### Serverless Framework

Then came the [Serverless Framework](https://www.serverless.com/) which I also had the opportunity to use in my job.  This is an open source project and it's similar to AWS Cloudformation in that you can write the instructions to provision your cloud infrastructure in a plain text file.  I found this more easier to write and read probably because it's less typing involved and less verbose?

Serverless framework is popular among developers for deploying AWS Lambda functions, which is probably why I like this better than AWS CloudFormation.  It will build, package and deploy code for you with one simple command: `serverless deploy`.

#### YAML
Below is a sample serverless yaml (**serverless.yml**) file:
```yaml
service: users

functions: # Your "Functions"
  usersCreate:
    events: # The "Events" that trigger this function
      - httpApi: 'POST /users/create'
  usersDelete:
    events:
      - httpApi: 'DELETE /users/delete'

resources: # The "Resources" your "Functions" use. Raw AWS CloudFormation goes in here.
```

It can be written in JSON format as well (**serverless.json**) just like in AWS CloudFormation.  In addition, which I didn't know until now, you can write it in JavaScript (**serverless.js**) and TypeScript (**serverless.ts**) too.  Man, this is getting better.

#### JavaScript
```js
'use strict';

// serverless.js

module.exports = {
  service: 'users',
  functions: {
    usersCreate: {
      events: [
        {
          httpApi: 'POST /users/create',
        },
      ],
    },
    // ...
  },
  resources: {},
};
```

#### TypeScript
```ts
// Requiring @types/serverless in your project package.json
import type { Serverless } from 'serverless/aws';

// serverless.ts

const serverlessConfiguration: Serverless = {
  service: 'users',
  functions: {
    usersCreate: {
      events: [
        {
          httpApi: 'POST /users/create',
        },
      ],
    },
    // ...
  },
  resources: {},
};

module.exports = serverlessConfiguration;
```

### AWS Cloud Development Kit
Now with [AWS Cloud Development Kit](https://aws.amazon.com/cdk/), or CDK, (I think it's the newer kid in this group if I'm not mistaken), you can write the instructions using familiar programming languages like **Python**, **Java**, and **C#**.  Yeah you read that right.  I'm a C# developer so maybe I can use this instead.

#### C#
So below is what a cloud stack in C# looks like.  With CDK, you create a cloud stack in your programming language.
```cs
using Amazon.CDK;
using Amazon.CDK.AWS.S3;

namespace HelloCdk
{
    public class HelloCdkStack : Stack
    {
        public HelloCdkStack(App scope, string id, IStackProps props=null) : base(scope, id, props)
        {
            new Bucket(this, "MyFirstBucket", new BucketProps
            {
                Versioned = true
            });
        }
    }
}
```

Then you run the `cdk synth` command to output the below CloudFormation template for you:
```yaml
Resources:
  MyFirstBucketB8884501:
    Type: AWS::S3::Bucket
    Properties:
      VersioningConfiguration:
        Status: Enabled
    UpdateReplacePolicy: Retain
    DeletionPolicy: Retain
    Metadata:...
```

To deploy, you just run the `cdk deploy` command.  I'm really liking this more than AWS CloudFormation for sure.  But compared to Serverless framework?  Well I have yet to use CDK before I can decide.

So which one do you prefer?  Whichever one you choose, I hope it's right for you.  I am just glad that we have these options, don't you think?


### References
* [AWS CloudFormation](https://aws.amazon.com/cloudformation/)
* [Serverless Framework](https://www.serverless.com/)
* [AWS Cloud Development Kit](https://aws.amazon.com/cdk/)
