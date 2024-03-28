# AWS CloudFormation

**AWS CloudFormation** is a service that helps you model and set up your AWS resources, allowing you to focus more on your applications that run in AWS. You create a template that describes all the AWS resources you want, like Amazon EC2 instances or Amazon RDS DB instances, and CloudFormation takes care of provisioning and configuring those resources for you.

## Simplify Infrastructure Management

- A template describes all your resources and their properties.
- When you use that template to create a CloudFormation stack, CloudFormation provisions the Auto Scaling group, load balancer, and database for you.
- After the stack has been successfully created, your AWS resources are up and running.
- You can delete the stack just as easily, which deletes all the resources in the stack.
- By using CloudFormation, you easily manage a collection of resources as a single unit.

## Quickly Replicate Your Infrastructure

- Reuse your CloudFormation template to create your resources in a consistent and repeatable manner.
- Describe your resources once and then provision the same resources over and over in multiple regions.

## Easily Control and Track Changes to Your Infrastructure

- When you provision your infrastructure with CloudFormation, the template describes exactly what resources are provisioned and their settings.
- These templates are text files, so you can track differences in your templates to track changes to your infrastructure, similar to how developers control revisions to source code.
- You can use a version control system with your templates to know exactly what changes were made, who made them, and when.
- If you need to reverse changes to your infrastructure, you can use a previous version of your template.

## Template Anatomy

A template is a JSON- or YAML-formatted text file that describes your AWS infrastructure. The following examples show an AWS CloudFormation template structure and its sections.

### JSON

The following example shows a JSON-formatted template fragment.

{
  "AWSTemplateFormatVersion" : "version date",
  "Description" : "JSON string",
  "Metadata" : {
    // template metadata
  },
  "Parameters" : {
    // set of parameters
  },
  "Rules" : {
    // set of rules
  },
  "Mappings" : {
    // set of mappings
  },
  "Conditions" : {
    // set of conditions
  },
  "Transform" : {
    // set of transforms
  },
  "Resources" : {
    // set of resources
  },
  "Outputs" : {
    // set of outputs
  }
}

## YAML-Formatted Template Fragment

AWSTemplateFormatVersion: "version date"

Description:
  String

Metadata:
   template metadata

Parameters:
   set of parameters

Rules:
   set of rules

Mappings:
   set of mappings

Conditions:
   set of conditions

Transform:
   set of transforms

Resources:
   set of resources

Outputs:
   set of outputs
