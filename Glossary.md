# Storage

### Comparison table highlighting the key differences between AWS S3, EFS, EBS, and Instance Store:

| Feature | AWS S3 | AWS EFS | AWS EBS | Instance Store |
|---------|--------|---------|---------|----------------|
| **Type** | Object storage | File storage | Block storage | Temporary block-level storage |
| **Use Case** | Web-based storage for large amounts of data, widely accessible | Shared file storage for use with AWS Cloud services and on-premises resources | High-performance block storage for use with EC2 and databases | Temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content |
| **Data Access** | Multiple systems or users concurrently | Multiple EC2 instances concurrently | Single EC2 instance at a time | Single EC2 instance at a time |
| **Performance** | High throughput, low latency with S3 Transfer Acceleration | High throughput, low latency over NFS | High IOPS, low latency, provisioned IOPS for intensive workloads | Very high IOPS, low latency, ideal for high-speed local storage |
| **Durability** | 99.999999999% (11 9's) | 99.999999999% (11 9's) | 99.999% | Data is lost if the instance is stopped or terminated |
| **Availability** | Designed for 99.99% availability | Designed for 99.99% availability | 99.5% - 99.99% | Varies, as it is physically attached to the host computer |
| **Scalability** | Virtually unlimited storage | Automatically scales with increasing files | Fixed size, but can be increased with some effort | Fixed size, tied to the instance |
| **Pricing** | Pay for what you use, with additional cost for retrieval and requests | Pay for what you use, no additional cost for throughput or requests | Pay for provisioned storage, with additional cost for IOPS and throughput | Included in the cost of the EC2 instance |
| **Data Persistence** | Persistent | Persistent | Persistent | Non-persistent |


# S3 Storage Classes

| Feature | S3 Standard | S3 Intelligent-Tiering | S3 Standard-IA | S3 One Zone-IA | S3 Glacier | S3 Glacier Deep Archive |
|---------|-------------|------------------------|----------------|----------------|------------|-------------------------|
| **Use Case** | General-purpose storage for frequently accessed data | Data with unknown or changing access patterns | Less frequently accessed data but needs to be readily available | Data that is infrequently accessed and can be stored in a single AZ | Long-term data archiving with occasional access | Long-term data archiving for rarely accessed data |
| **Durability** | 99.999999999% | 99.999999999% | 99.999999999% | 99.999999999% | 99.999999999% | 99.999999999% |
| **Availability Zones** | Multiple | Multiple | Multiple | Single | Multiple | Multiple |
| **Minimum Storage Duration** | None | None | 30 days | 30 days | 90 days | 180 days |
| **Minimum Billable Object Size** | None | None | 128KB | 128KB | 40KB | 40KB |
| **Retrieval Fee** | None | None | Per GB retrieved | Per GB retrieved | Per GB retrieved | Per GB retrieved |
| **First Byte Latency** | Milliseconds | Milliseconds | Milliseconds | Milliseconds | Minutes to hours | Hours |
| **Data Resilience** | Stored redundantly across multiple devices in multiple facilities | Automatically moves data to the most cost-effective tier | Lower cost for infrequently accessed data | Lower cost option for infrequently accessed data not requiring multi-AZ resilience | Secure and durable storage for data archiving | Lowest cost storage for long-term archiving |
| **Lifecycle Transition** | Supported | Supported | Supported | Supported | Supported | Supported |
| **Versioning** | Supported | Supported | Supported | Supported | Supported | Supported |
| **Event Notifications** | Supported | Supported | Supported | Supported | Supported | Supported |
| **Resilient Against Disasters** | Yes | Yes | Yes | No (single AZ) | Yes | Yes |
| **Data Encryption** | Supported | Supported | Supported | Supported | Supported | Supported |
| **Access Control** | Fine-grained | Fine-grained | Fine-grained | Fine-grained | Fine-grained | Fine-grained |
| **Monitoring and Logging** | Detailed | Detailed | Detailed | Detailed | Detailed | Detailed |
| **Performance** | High throughput and low latency | Adapts based on access patterns | Lower throughput than Standard | Lower throughput than Standard | Lowest throughput | Lowest throughput |
| **Pricing** | Higher cost for storage | Cost varies based on access | Lower storage cost than Standard | Lower storage cost than Standard and Standard-IA | Low storage cost with higher retrieval fees | Lowest storage cost with highest retrieval fees |

# RDS vs Dynamo DB vs Redshift

| Feature | Amazon RDS | Amazon DynamoDB | Amazon Redshift |
|---------|------------|-----------------|-----------------|
| **Type** | Relational Database Service | NoSQL Database | Data Warehouse Service |
| **Database Models** | SQL, MySQL, PostgreSQL, Oracle, MariaDB, and Aurora | Key-Value and Document Store | Column-oriented |
| **Use Cases** | Traditional applications, ERP, CRM, e-commerce | High-traffic web apps, IoT, mobile apps, gaming | Business intelligence, data analysis, reporting |
| **Performance** | High performance for transactional workloads | High performance, fast and consistent response times | Optimized for complex queries over large datasets |
| **Storage** | Up to 64 TB | Unlimited | Up to 8 PB |
| **Scaling** | Vertical scaling | Horizontal scaling, auto-scaling | Horizontal scaling |
| **Data Replication** | Multi-AZ deployment for high availability | Multi-region, multi-master replication | Snapshot and restore to new clusters |
| **Backup and Restore** | Automated backups, database snapshots | On-demand backup and restore, point-in-time recovery | Automated and manual snapshots |
| **Security** | Encryption at rest and in transit, IAM for access control | Encryption at rest and in transit, fine-grained access control | Encryption at rest and in transit, VPC for network isolation |
| **Pricing** | Pay for compute and storage resources | Pay for read/write throughput and storage | Pay for compute nodes and storage |
| **Maintenance** | Managed maintenance and updates | Fully managed, no server management | Managed maintenance and updates |
| **Integration** | Broad integration with AWS services | Integrates with other AWS services | Integrates with other AWS services, optimized for use with S3 |


# Amazon Machine Image

An Amazon Machine Image (AMI) is a supported and maintained image provided by AWS that provides the information required to launch an instance. You must specify an AMI when you launch an instance. You can launch multiple instances from a single AMI when you require multiple instances with the same configuration. You can use different AMIs to launch instances when you require instances with different configurations.

## An AMI includes the following:

One or more Amazon Elastic Block Store (Amazon EBS) snapshots, or, for instance-store-backed AMIs, a template for the root volume of the instance (for example, an operating system, an application server, and applications).

Launch permissions that control which AWS accounts can use the AMI to launch instances.

A block device mapping that specifies the volumes to attach to the instance when it's launched.

### Use an AMI

The following diagram summarizes the AMI lifecycle. After you create and register an AMI, you can use it to launch new instances. (You can also launch instances from an AMI if the AMI owner grants you launch permissions.) You can copy an AMI within the same AWS Region or to different AWS Regions. When you no longer require an AMI, you can deregister it.

![alt text](image-5.png)
			
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html

# EC2 pricing options

| Pricing Option | Description | Use Cases | Commitment | Savings Potential | Additional Points |
|----------------|-------------|-----------|------------|-------------------|-------------------|
| **On-Demand** | Pay for compute capacity by the hour or second with no long-term commitments. | Ideal for short-term, irregular workloads that cannot be interrupted. | None | None | Most flexible option, highest cost, instant availability. |
| **Reserved Instances** | Reserve instances for a 1 or 3-year term and get a significant discount over On-Demand rates. | Best for steady-state usage and applications with predictable usage. | 1 or 3 years | Up to 75% | Options for partial, all upfront, or no upfront payment. |
| **Savings Plans** | Commit to a consistent amount of usage (measured in $/hour) for a 1 or 3-year period and receive a lower rate. | Flexible usage across instance families and AWS regions. | 1 or 3 years | Up to 72% | Compute Savings Plans and EC2 Instance Savings Plans available. |
| **Spot Instances** | Purchase unused EC2 capacity at a steep discount. Instances can be interrupted by AWS with two minutes of notification. | Suitable for flexible start and end times, fault-tolerant applications, and data analysis. | None | Up to 90% | Best for workloads with flexible timing, significant cost savings. |
| **Dedicated Hosts** | Physical EC2 servers dedicated for your use which can help you meet compliance requirements. | Useful when you have server-bound software licenses that could complicate multi-tenant virtualization. | Per hour or reservation | Varies | Useful for regulatory or compliance needs, allows for existing license utilization. |
| **Dedicated Instances** | Instances run on hardware that's dedicated to a single customer. | When you need to ensure your instances are physically isolated at the host hardware level from instances that belong to other AWS accounts. | Per hour | Varies | Physical isolation meets certain compliance requirements. |
| **Capacity Reservations** | Reserve capacity for your EC2 instances in a specific Availability Zone for any duration. | When you need to ensure you have EC2 capacity when you need it, for as long as you need it. | None | Varies | Good for applications that require reserved capacity. |


# AWS Security Services

| Service | Description | Use Cases | Key Features |
|---------|-------------|-----------|--------------|
| **AWS IAM** | Manages access to AWS services and resources securely. | User and group management, access policies, multi-factor authentication. | Granular permissions, policy simulation, integration with other AWS services. |
| **Amazon Cognito** | Provides user sign-up, sign-in, and access control to web and mobile applications. | User directory management, social identity provider integration, user data synchronization. | User pools, identity pools, federation with social identity providers. |
| **AWS KMS** | Manages cryptographic keys for your applications. | Encryption key management, key rotation, key usage policies. | Hardware security modules, automated key rotation, integration with AWS services. |
| **AWS Shield** | Protects against DDoS attacks. | DDoS protection for AWS services, automatic attack mitigation, real-time visibility into attacks. | Always-on detection, inline mitigation, cost protection. |
| **Amazon Inspector** | Automated security assessment service to help improve the security and compliance of applications deployed on AWS. | Vulnerability detection, security best practices enforcement, application scanning. | Automated assessments, detailed findings, integration with AWS services. |
| **AWS WAF** | Web application firewall that helps protect web applications from common web exploits. | Rule management for web traffic filtering, real-time metrics and logging, automated web security. | Customizable web security rules, real-time visibility, rate-based rules. |
| **Amazon GuardDuty** | Threat detection service that continuously monitors for malicious activity and unauthorized behavior. | Anomaly detection, threat prioritization, integrated threat intelligence. | Machine learning, anomaly detection, integrated threat intelligence feeds. |
| **AWS Security Hub** | Centralized view of your security alerts and security posture across your AWS accounts. | Aggregated security findings, compliance checks, automated remediation. | Comprehensive security and compliance checks, automated response and remediation. |
| **AWS Audit Manager** | Helps you continuously audit your AWS usage to simplify how you assess risk and compliance. | Audit evidence collection, compliance monitoring, audit preparation. | Prebuilt frameworks for compliance, automated evidence collection, continuous auditing. |

# AWS CloudFormation

AWS CloudFormation is an automated provisioning engine designed to deploy resources consistently and repeatably across various AWS services. It enables developers and system administrators to create and manage a collection of related AWS resources by provisioning and updating them in an orderly and predictable fashion.

## Key Benefits of AWS CloudFormation

- **Infrastructure as Code**: Manage and provision your infrastructure through text files which can be version controlled, shared, and reused.

- **Automation**: Automate the creation and destruction of resources which can lead to a more efficient development process.

- **Consistency and Reproducibility**: Ensure your environments are provisioned consistently without manual errors or variations.

- **Safety and Control**: Roll back changes automatically if errors are detected during deployment, providing a safety net for deployments.

- **Integration with AWS Services**: Works seamlessly with other AWS services, enhancing overall service management.

- **Customization**: Customize templates to create unique environments and use parameters to input custom values during stack creation.

- **Management of Stack Resources**: Easily manage, update, and delete an entire stack as a single unit rather than managing resources individually.

- **Cost Tracking**: Associate costs with stacks and track them by tags for more detailed financial administration.

- **Change Sets**: Preview changes to your stack before implementation, allowing for better planning and risk management.

- **Nested Stacks**: Organize complex stacks by nesting them, simplifying management and replication of stacks.

- **Cross-Region and Account Deployment**: Deploy resources across different regions and AWS accounts from a single template.

- **Drift Detection**: Detect when your stack's actual configuration differs from its expected configuration.

- **Resource Import**: Bring existing AWS resources into CloudFormation management without needing to recreate them.

- **Declarative Programming**: Define what the end state should look like and let CloudFormation handle the provisioning and configuration.

- **Community Templates**: Leverage a wide range of community-contributed templates to get started quickly with best practices.

- **Compliance and Governance**: Enforce compliance with company policies and governance by controlling the resources that can be provisioned.

AWS CloudFormation provides a robust solution for managing infrastructure, allowing teams to focus on building applications rather than managing infrastructure.
