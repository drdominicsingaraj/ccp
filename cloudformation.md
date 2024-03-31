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

```json
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
```

### YAML-Formatted Template Fragment

```yaml
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

```

## Template Sections

Templates include several major sections. The **Resources** section is the only required section. Some sections in a template can be in any order. However, as you build your template, it can be helpful to use the logical order shown in the following list because values in one section might refer to values from a previous section.

### Format Version (optional)

The AWS CloudFormation template version that the template conforms to. The template format version isn't the same as the API or WSDL version. The template format version can change independently of the API and WSDL versions.

### AWS CloudFormation Template Content

#### JSON Format

```json
{
  "AWSTemplateFormatVersion": "2010-09-09",
  "Description": "Here are some details about the template.",
  "Metadata": {
    "Instances": {
      "Description": "Information about the instances"
    },
    "Databases": {
      "Description": "Information about the databases"
    }
  },
  "Parameters": {
    "InstanceTypeParameter": {
      "Type": "String",
      "Default": "t2.micro",
      "AllowedValues": ["t2.micro", "m1.small", "m1.large"],
      "Description": "Enter t2.micro, m1.small, or m1.large. Default is t2.micro."
    }
  },
  "Ec2Instance": {
    "Type": "AWS::EC2::Instance",
    "Properties": {
      "InstanceType": {
        "Ref": "InstanceTypeParameter"
      },
      "ImageId": "ami-0ff8a91507f77f867"
    }
  }
}
```

#### YAML Format

```yaml

AWSTemplateFormatVersion: "2010-09-09"
Description: >
  Here are some
  details about
  the template.
Metadata:
  Instances:
    Description: "Information about the instances"
  Databases: 
    Description: "Information about the databases"
Parameters:
  InstanceTypeParameter:
    Type: String
    Default: t2.micro
    AllowedValues:
      - t2.micro
      - m1.small
      - m1.large
    Description: Enter t2.micro, m1.small, or m1.large. Default is t2.micro.
Ec2Instance:
  Type: AWS::EC2::Instance
  Properties:
    InstanceType:
      Ref: InstanceTypeParameter
    ImageId: ami-0ff8a91507f77f867
```

![Cloudformation Stack](images/stackparameters.png)

```yaml

Rules:
  testInstanceType:
    RuleCondition: !Equals 
      - !Ref Environment
      - test
    Assertions:
      - Assert:
          'Fn::Contains':
            - - a1.medium
            - !Ref InstanceType
        AssertDescription: 'For a test environment, the instance type must be a1.medium'
  prodInstanceType:
    RuleCondition: !Equals 
      - !Ref Environment
      - prod
    Assertions:
      - Assert:
          'Fn::Contains':
            - - a1.large
            - !Ref InstanceType
        AssertDescription: 'For a production environment, the instance type must be a1.large'

```

#### AWS Rule Functions

In the condition or assertions of a rule, you can use intrinsic functions, such as `Fn::Equals`, `Fn::Not`, and `Fn::RefAll`. The condition property determines if AWS CloudFormation applies the assertions. If the condition evaluates to true, CloudFormation evaluates the assertions to verify whether a parameter value is valid when a provisioned product is created or updated. If a parameter value isn't valid, CloudFormation doesn't create or update the stack. If the condition evaluates to false, CloudFormation doesn't check the parameter value and proceeds with the stack operation.

##### Functions

- `Fn::And`
- `Fn::Contains`
- `Fn::EachMemberEquals`
- `Fn::EachMemberIn`
- `Fn::Equals`
- `Fn::Not`
- `Fn::Or`
- `Fn::RefAll`
- `Fn::ValueOf`
- `Fn::ValueOfAll`
- Supported Functions
- Supported Attributes

#### Mappings (optional)

A mapping of keys and associated values that you can use to specify conditional parameter values, similar to a lookup table. You can match a key to a corresponding value by using the `Fn::FindInMap` intrinsic function in the Resources and Outputs sections.

```json

{
  "AWSTemplateFormatVersion": "2010-09-09",
  "Mappings": {
    "RegionMap": {
      "us-east-1": {
        "HVM64": "ami-0ff8a91507f77f867",
        "HVMG2": "ami-0a584ac55a7631c0c"
      },
      "us-west-1": {
        "HVM64": "ami-0bdb828fd58c52235",
        "HVMG2": "ami-066ee5fd4a9ef77f1"
      },
      "eu-west-1": {
        "HVM64": "ami-047bb4163c506cd98",
        "HVMG2": "ami-0a7c483d527806435"
      },
      "ap-northeast-1": {
        "HVM64": "ami-06cd52961ce9f0d85",
        "HVMG2": "ami-053cdd503598e4a9d"
      },
      "ap-southeast-1": {
        "HVM64": "ami-08569b978cc4dfa10",
        "HVMG2": "ami-0be9df32ae9f92309"
      }
    }
  },
  "Resources": {
    "myEC2Instance": {
      "Type": "AWS::EC2::Instance",
      "Properties": {
        "ImageId": {
          "Fn::FindInMap": [
            "RegionMap",
            {
              "Ref": "AWS::Region"
            },
            "HVM64"
          ]
        },
        "InstanceType": "m1.small"
      }
    }
  }
}
```

#### Conditions (optional)

**Conditions** control whether certain resources are created or whether certain resource properties are assigned a value during stack creation or update. For example, you could conditionally create a resource that depends on whether the stack is for a **production** or **test environment**.

```yaml

AWSTemplateFormatVersion: 2010-09-09
Parameters:
  EnvType:
    Description: Environment type.
    Default: test
    Type: String
    AllowedValues:
      - prod
      - test
    ConstraintDescription: must specify prod or test.
Conditions:
  CreateProdResources: !Equals 
    - !Ref EnvType
    - prod
Resources:
  EC2Instance:
    Type: 'AWS::EC2::Instance'
    Properties:
      ImageId: ami-0ff8a91507f77f867
  MountPoint:
    Type: 'AWS::EC2::VolumeAttachment'
    Condition: CreateProdResources
    Properties:
      InstanceId: !Ref EC2Instance
      VolumeId: !Ref NewVolume
      Device: /dev/sdh
  NewVolume:
    Type: 'AWS::EC2::Volume'
    Condition: CreateProdResources
    Properties:
      Size: 100
      AvailabilityZone: !GetAtt 
        - EC2Instance
        - AvailabilityZone

```

#### Transform (optional)

For serverless applications (also referred to as Lambda-based applications), **Transform** specifies the version of the **AWS Serverless Application Model (AWS SAM)** to use. When you specify a transform, you can use AWS SAM syntax to declare resources in your template. The model defines the syntax that you can use and how it's processed.

You can also use `AWS::Include` transforms to work with template snippets that are stored separately from the main AWS CloudFormation template. You can store your snippet files in an Amazon S3 bucket and then reuse the functions across multiple templates.

#### Resources (required)

Specifies the stack resources and their properties, such as an Amazon Elastic Compute Cloud instance or an Amazon Simple Storage Service bucket. You can refer to resources in the Resources and Outputs sections of the template.

```yaml
Resources:
  MyEC2Instance:
    Type: "AWS::EC2::Instance"
    Properties:
      ImageId: "ami-0ff8a91507f77f867"

```

#### Outputs (optional)

Describes the values that are returned whenever you view your stack’s properties. For example, you can declare an output for an S3 bucket name and then call the aws cloudformation describe-stacks AWS CLI command to view the name.

```yaml

Outputs:
  BackupLoadBalancerDNSName:
    Description: The DNSName of the backup load balancer
    Value: !GetAtt BackupLoadBalancer.DNSName
    Condition: CreateProdResources
  InstanceID:
    Description: The Instance ID
    Value: !Ref EC2Instance

```

## Cloudformation Stack Creation

There are several ways to create an AWS CloudFormation stack, each suited to different use cases and preferences:

| Method | Description |
| --- | --- |
| **AWS Management Console** | Use the CloudFormation console to create a stack by selecting a template, setting parameters, and configuring options through a web interface. |
| **AWS Command Line Interface (CLI)** | Run the `aws cloudformation create-stack` command with the necessary parameters and template location. Useful for automation scripts and command-line tools. |
| **AWS CloudFormation API** | Invoke the `CreateStack` action directly through the API for custom applications or tools that manage CloudFormation stacks. |
| **Infrastructure as Code (IaC) Tools** | Utilize third-party IaC tools like Terraform or Pulumi, which can interact with CloudFormation and provide additional features. |
| **AWS Systems Manager** | Create a stack directly from a Systems Manager document if using AWS Systems Manager. |
| **AWS SDKs** | Use the AWS Software Development Kits (SDKs) for programming languages to create stacks programmatically from application code. |
| **AWS CloudFormation Templates** | Start with a sample template or create your own to define the resources you want to provision and manage as a stack. |
| **AWS Service Catalog** | Create a stack as part of provisioning a product if you have predefined products in the AWS Service Catalog. |

### AWS Management Console

| Step | Action |
| --- | --- |
| 1. **Access the Console** | Open the AWS CloudFormation console at `console.aws.amazon.com/cloudformation`. |
| 2. **Create Stack** | Select **Create Stack** to initiate a new stack creation. |
| 3. **Choose Template** | Choose a template that describes the AWS resources you want to create. You can select a sample template provided by AWS or upload your custom template. |
| 4. **Specify Parameters** | Provide the stack name and input parameters. Parameters must be separated by space, and key names are case-sensitive. |
| 5. **Configure Options** | Configure additional options like tags, permissions, and other advanced settings. |
| 6. **Review** | Check all the details you've entered and make any necessary adjustments. |
| 7. **Create the Stack** | Click on **Create Stack** to deploy your resources as defined in the template. |

Remember to use the `NoEcho` property for sensitive information like passwords to prevent them from being returned in outputs.

For a command-line approach, you can use the `aws cloudformation create-stack` command with the necessary parameters and template location.

### AWS Command Line Interface

To set up an Apache web server using AWS CloudFormation via the AWS CLI, you'll need to create a CloudFormation template that defines the resources, and then use the CLI to create a stack with that template.

Here's a basic example of how you might define the resources in a CloudFormation template (save this as `apache_web_server.yaml`):

```yaml
AWSTemplateFormatVersion: '2024-31-03'
Description: A simple AWS CloudFormation template to deploy an Apache web server.

Resources:
  WebServerInstance:
    Type: 'AWS::EC2::Instance'
    Properties:
      ImageId: 'ami-0abcdef1234567890' # Replace with a valid Amazon Linux AMI ID for your region
      InstanceType: t2.micro
      SecurityGroups:
        - Ref: WebServerSecurityGroup
      UserData:
        Fn::Base64: !Sub |
          #!/bin/bash
          yum update -y
          yum install -y httpd
          systemctl start httpd
          systemctl enable httpd
          echo "Hello World from $(hostname -f)" > /var/www/html/index.html

  WebServerSecurityGroup:
    Type: 'AWS::EC2::SecurityGroup'
    Properties:
      GroupDescription: Enable HTTP access
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: '80'
          ToPort: '80'
          CidrIp: 0.0.0.0/0
```

This template will create an EC2 instance and install Apache web server on it. The `UserData` section includes a script that updates the system, installs Apache, starts the service, and creates a simple index.html page.

Once you have your template, you can use the following AWS CLI command to create the CloudFormation stack:

```bash
aws cloudformation create-stack --stack-name MyApacheWebServerStack --template-body file://apache_web_server.yaml
```

Replace `MyApacheWebServerStack` with your desired stack name. The `--template-body` parameter points to the file path of your CloudFormation template.

Please ensure you have the AWS CLI installed and configured with the necessary permissions to create these resources. Also, replace the `ImageId` with a valid Amazon Linux AMI ID for your AWS region.

### AWS SDK (Boto3)

To set up an Apache web server using the AWS CloudFormation SDK, you’ll need to write a script that utilizes the SDK to interact with AWS CloudFormation. Below is an example in Python using the Boto3 library, which is the AWS SDK for Python.

First, make sure you have Boto3 installed:

`pip install boto3`

Then, you can use the following Python script as a starting point:

```python
import boto3

# Initialize a session using your AWS credentials
aws_session = boto3.Session(
    aws_access_key_id='YOUR_ACCESS_KEY',
    aws_secret_access_key='YOUR_SECRET_KEY',
    region_name='YOUR_REGION'
)

# Create a CloudFormation client
cf_client = aws_session.client('cloudformation')

# Define the CloudFormation template for setting up an Apache web server
apache_web_server_template = """
AWSTemplateFormatVersion: '2010-09-09'
Description: A simple AWS CloudFormation template to deploy an Apache web server.

Resources:
  WebServerInstance:
    Type: 'AWS::EC2::Instance'
    Properties:
      ImageId: 'ami-0abcdef1234xxxxxx' # Replace with a valid Amazon Linux AMI ID for your region
      InstanceType: t2.micro
      SecurityGroups:
        - Ref: WebServerSecurityGroup
      UserData:
        Fn::Base64: !Sub |
          #!/bin/bash
          yum update -y
          yum install -y httpd
          systemctl start httpd
          systemctl enable httpd
          echo "Hello World from $(hostname -f)" > /var/www/html/index.html

  WebServerSecurityGroup:
    Type: 'AWS::EC2::SecurityGroup'
    Properties:
      GroupDescription: Enable HTTP access
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: '80'
          ToPort: '80'
          CidrIp: 0.0.0.0/0
"""

# Create the CloudFormation stack
response = cf_client.create_stack(
    StackName='ApacheWebServerStack',
    TemplateBody=apache_web_server_template,
    Parameters=[
        {
            'ParameterKey': 'KeyName',
            'ParameterValue': 'your-key-pair-name'
        },
    ],
    TimeoutInMinutes=123,
    Capabilities=[
        'CAPABILITY_IAM', 'CAPABILITY_NAMED_IAM'
    ],
    OnFailure='ROLLBACK'
)

print(response)
```

Replace `YOUR_ACCESS_KEY`, `YOUR_SECRET_KEY`, and `YOUR_REGION` with your AWS credentials and desired region. Also, replace `ami-0abcdef1234xxxxxx` with a valid Amazon Linux AMI ID for your region and `your-key-pair-name` with your EC2 key pair name.

This script initializes a session with your AWS credentials, creates a CloudFormation client, defines a template for an Apache web server, and then creates a stack with that template.

Please ensure you have the necessary permissions to create these resources and manage stacks in AWS CloudFormation.

## AWS CloudFormation Sample Templates

Use sample AWS CloudFormation templates to learn how to declare specific AWS resources or solve a particular use case. We recommend that you use sample templates as a starting point for creating your own templates, not for launching production-level environments. Before launching a template, always review the resources that it will create and the permissions it requires.

![Cloudformation Sample Templates](images/cftemplates.png)

Reference :

```markdown
[AWS CloudFormation Templates](https://github.com/awslabs/aws-cloudformation-templates.git)
```
