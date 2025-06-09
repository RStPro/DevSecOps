﻿CloudFormation is an Amazon Web Services (AWS) IaC tool for automated provision and resource management.
﻿﻿Instead of manually configuring resources through the AWS Management Console or using the AWS Command Line Interface (CLI), you can use CloudFormation templates to describe your infrastructure in a "declarative" manner.

## Declarative Infrastructure as Code

With CloudFormation, you express the desired state of your infrastructure using a JSON or YAML template. This template defines the resources, their configurations, and the relationships between them.
CloudFormation provides and manages these resources, making managing and replicating your infrastructure easier.

## Templates and Stacks

A CloudFormation template is a text file that serves as a blueprint for your infrastructure.
It contains sections that describe various AWS resources like EC2 instances, S3 buckets, and more.
When you use a template to create resources, it forms a CloudFormation stack.
Stacks are the fundamental units of CloudFormation, and they represent a collection of AWS resources that are created, updated, and deleted together.

**Example**

```bash
# CloudFormation Template
AWSTemplateFormatVersion: '2010-09-09'  # Version of the CloudFormation template syntax

Description: 'A simple CloudFormation template'  # Description of the template

Resources:  # Section where AWS resources are defined
  MyEC2Instance:  # Logical name of the resource
    Type: 'AWS::EC2::Instance'  # Type of AWS resource being created

    Properties:  # Properties specific to the resource type
      ImageId: 'ami-12345678'  # ID of the Amazon Machine Image (AMI) for the EC2 instance
      InstanceType: 't2.micro'  # Type of EC2 instance
      KeyName: 'my-key-pair'  # SSH key pair for accessing the instance

  MyS3Bucket:  # Another resource example
    Type: 'AWS::S3::Bucket'
    Properties:
      BucketName: 'my-s3-bucket'  # Name of the S3 bucket

Outputs:  # Section to define outputs for the template
  EC2InstanceId:  # Logical name for the output
    Description: 'ID of the EC2 instance'  # Description of the output
    Value: !Ref MyEC2Instance  # Reference to the EC2 instance resource
```

- **AWSTemplateFormatVersion:** This specifies the CloudFormation template version.
- **Description:** Provides a brief description of the template.
- **Resources:** This section defines the AWS resources to be created, such as EC2 instances or S3 buckets. Each resource has a logical name (MyEC2Instance, MyS3Bucket). Type indicates the AWS resource type. Properties hold configuration settings for the resource.
- **Outputs:** This section defines the output values displayed after creating the stack. Logical name, description, and a reference to a resource using `!Ref`.

**Notes:** CloudFormation Designer is a service for visually creating/validating these templates. Read more [here](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/working-with-templates-cfn-designer-overview.html).  

## CloudFormation Architecture

Similar to Terraform, CloudFormation follows a workflow for provision and management. To better understand the workflow, we need to understand the inner workings of CloudFormation and its Architecture. 

## Main and Worker Architecture

CloudFormation employs a main-worker architecture. The main, typically a CloudFormation service running in AWS, interprets and processes the CloudFormation template. It manages the overall stack creation, update, or deletion orchestration. The worker nodes, distributed across AWS regions, are responsible for carrying out the actual provisioning of resources.

## Template Processing Flow

![[Pasted image 20250609180846.png]]

- **Template Submission:** users submit a CloudFormation template, written in JSON or YAML, to the CloudFormation service. The template specifies the desired AWS resources and their configurations. This can be stored in an [S3](https://aws.amazon.com/s3/) bucket, for example.
- **Template Validation:** the CloudFormation service validates the submitted template to ensure its syntax is correct and it follows AWS resource specifications.
- **Processing by the Main Node:** the main node processes the template, creating a set of instructions for resource provisioning. It determines the order in which resources should be created based on dependencies.
- **Resource Provisioning:** the main node communicates with worker nodes distributed across different AWS regions. Worker nodes carry out the actual provisioning of resources stated by the instructions provided by the main.
- **Stack Creation/Update:** the resources are created or updated in the specified order, forming a stack. The stack represents the complete set of provisioned resources.

## Event-Driven Model

CloudFormation operates on an event-driven model. Events are generated during stack creation, update, or deletion processes, and CloudFormation logs these events. Users can monitor these events to track the progress of stack operations or identify any issues.

## Rollback and Rollback Triggers

If an error occurs during the stack creation or update process, CloudFormation can automatically trigger a [rollback](https://docs.aws.amazon.com/autoscaling/ec2/userguide/instance-refresh-rollback.html), reverting the stack to its previous state. Rollback triggers can be defined in the template to specify conditions under which a rollback should occur.

## Cross-Stack References

CloudFormation supports cross-stack references, allowing resources from one stack to refer to resources in another. This is useful for managing complex applications and dependencies that span multiple stacks.

Understanding the architecture of CloudFormation provides insights into how the service efficiently manages the orchestration and provisioning of AWS resources, ensuring a reliable and consistent infrastructure deployment process.