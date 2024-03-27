# Glossary

## Cloud Service Models Comparison

| Service Model | Description | Customer Responsibility | Provider Responsibility | AWS Examples | Pros | Cons |
|---------------|-------------|-------------------------|-------------------------|--------------|------|------|
| **IaaS (Infrastructure as a Service)** | Provides virtualized computing resources over the internet. | Applications, Data, Runtime, Middleware, OS | Virtualization, Servers, Storage, Networking | Amazon EC2, Amazon S3 | High control of underlying resources, flexible | Requires more management |
| **PaaS (Platform as a Service)** | Offers hardware and software tools over the internet, typically for application development. | Applications, Data | Runtime, Middleware, OS, Virtualization, Servers, Storage, Networking | AWS Elastic Beanstalk, AWS Lambda | Easier to manage, focus on development | Less control over the environment |
| **SaaS (Software as a Service)** | Delivers software over the internet on a subscription basis. | None | Applications, Data, Runtime, Middleware, OS, Virtualization, Servers, Storage, Networking | Amazon WorkSpaces, Amazon Chime | Minimal responsibility, quick setup | Least control, dependent on provider |

Each cloud service model offers different levels of control, flexibility, and management, which can be selected based on the needs of the business or application. IaaS provides the most control but requires more management, PaaS eases the management burden but offers less control, and SaaS offers the least control but is the easiest to use and set up.

![Pizza as a Service Analogy](image-4.png)

[Pizza as a Service 2.0](https://engineering.dunelm.com/pizza-as-a-model-453b838ca165)

## Shared Responsibility Model

![Shared Responsibility Model](image-6.png)

[Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/)

## Storage Services

### AWS S3 vs EFS vs EBS vs Instance Store

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

## S3 Storage Classes

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

## AWS Virtual Private Cloud (VPC) and Related Components

| Component | Description | Additional Points |
|-----------|-------------|-------------------|
| **VPC** | A virtual network dedicated to your AWS account within the AWS Cloud. | Supports both IPv4 and IPv6 addressing. |
| **Subnets** | Subdivisions of your VPC where you can launch AWS resources. | Can be public or private, depending on the route table and network gateway associations. |
| **Route Tables** | Define rules, known as routes, that determine where network traffic from your subnets or gateways is directed. | Each subnet must be associated with a route table, which can be shared. |
| **Internet Gateways** | Connects your VPC to the internet and to other AWS services. | Enables communication between instances in your VPC and the internet. |
| **NAT Gateways** | Enable instances in a private subnet to connect to the internet or other AWS services but prevent the internet from initiating connections with the instances. | Provides a mechanism for instances in a private subnet to send outbound traffic. |
| **Security Groups** | Act as a virtual firewall for your instances to control inbound and outbound traffic. | Operates at the instance level and supports allow rules only. |
| **Network ACLs** | Provide a layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets. | Operates at the subnet level and supports both allow and deny rules. |
| **VPC Endpoints** | Enable private connections between your VPC and supported AWS services and VPC endpoint services powered by AWS PrivateLink. | Eliminates the need to use an Internet Gateway, NAT device, VPN connection, or AWS Direct Connect connection to communicate with AWS services. |
| **Elastic IP Addresses** | Static IPv4 addresses for dynamic cloud computing. | Can be associated with instances or network interfaces. |
| **Elastic Network Interfaces (ENIs)** | Virtual network interfaces that you can attach to instances in your VPC. | Can include primary and secondary private IP addresses, Elastic IP addresses, and security groups. |
| **VPC Peering** | Allows you to connect one VPC with another via a direct network route using private IP addresses. | Traffic between peered VPCs remains private and does not traverse the public internet. |
| **Transit Gateway** | Enables you to connect your VPCs and on-premises networks through a central hub. | Simplifies network architecture and reduces operational overhead. |
| **VPC Flow Logs** | Capture information about the IP traffic going to and from network interfaces in your VPC. | Helps monitor and troubleshoot connectivity issues. |
| **Traffic Mirroring** | Copy network traffic from network interfaces and send it to security and monitoring appliances for deep packet inspection. | Useful for content inspection and threat monitoring. |
| **VPN Connections** | Connect your VPCs to your on-premises networks using AWS Virtual Private Network (AWS VPN). | Provides secure and private sessions with IP Security (IPSec) and Transport Layer Security (TLS). |

For more detailed information on AWS VPC and its components, you can refer to the [AWS VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html) and [What is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) provided by AWS.

## AWS Global Infrastructure

AWS Global Infrastructure encompasses a variety of services and locations worldwide, ensuring high availability, security, and low-latency performance for AWS customers.

### AWS Global Infrastructure Components

| Component | Description | Examples |
|-----------|-------------|----------|
| **Regions** | Geographic locations around the world hosting AWS services. | US East (N. Virginia), Europe (Ireland), Asia Pacific (Sydney) |
| **Availability Zones** | Isolated data centers within each region to provide fault tolerance and stability. | Multiple AZs per region, each with independent power, cooling, and physical security |
| **CloudFront POPs** | Global network locations that cache content closer to users to reduce latency. | Over 600 POPs worldwide |
| **Regional Edge Caches** | Caching layers that sit between the origin server and the global edge locations. | Located in strategic regions to optimize content delivery |
| **Local Zones** | Extensions of AWS Regions placed closer to end-users to provide single-digit millisecond latency. | Los Angeles, Boston, Houston |
| **Direct Connect Locations** | Facilities that allow a dedicated network connection from on-premises to AWS. | Over 135 locations globally |
| **Wavelength Zones** | Infrastructure deployments within telecommunications providers' data centers at the edge of the 5G network. | Designed for ultra-low latency applications |
| **Countries & Territories Served** | The reach of AWS services across the globe. | Over 245 countries and territories |

![AWS Global Infrastructure](image-7.png)

AWS continues to expand its infrastructure to provide a robust platform for deploying applications and services globally. For more information, visit the [AWS Global Infrastructure page](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/).

### Key Features

- **Security**: AWS infrastructure is designed to be one of the most flexible and secure cloud computing environments available today.
- **Reliability**: AWS's high-availability data center architecture is designed to maximize reliability and minimize outages.
- **Performance**: AWS provides low-latency networking and high-speed connectivity across different regions and services.
- **Scalability**: Easily scale your applications up or down based on demand, across the globe.

### Global Reach

- AWS has announced plans for more Availability Zones and Regions, expanding its global presence to serve a wider audience.
- AWS infrastructure supports millions of active customers and a broad spectrum of use cases across virtually every industry.

For more information on AWS Global Infrastructure, you can visit the AWS Global Infrastructure page.

## RDS vs Dynamo DB vs Redshift

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

## Amazon Machine Image

An Amazon Machine Image (AMI) is a supported and maintained image provided by AWS that provides the information required to launch an instance. You must specify an AMI when you launch an instance. You can launch multiple instances from a single AMI when you require multiple instances with the same configuration. You can use different AMIs to launch instances when you require instances with different configurations.

### An AMI includes the following

One or more Amazon Elastic Block Store (Amazon EBS) snapshots, or, for instance-store-backed AMIs, a template for the root volume of the instance (for example, an operating system, an application server, and applications).

Launch permissions that control which AWS accounts can use the AMI to launch instances.

A block device mapping that specifies the volumes to attach to the instance when it's launched.

### Use an AMI

The following diagram summarizes the AMI lifecycle. After you create and register an AMI, you can use it to launch new instances. (You can also launch instances from an AMI if the AMI owner grants you launch permissions.) You can copy an AMI within the same AWS Region or to different AWS Regions. When you no longer require an AMI, you can deregister it.

![alt text](image-5.png)

<https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html>

### Types of AWS AMIs

AWS AMIs are essential for creating virtual machines within the AWS ecosystem. They contain the information necessary to boot and run instances.

#### AMI Categories

| AMI Type | Description | Use Cases |
|----------|-------------|-----------|
| **Amazon EBS-Backed AMI** | The root device for an instance launched from the AMI is an Amazon EBS volume created from an EBS snapshot. | Recommended for applications that require persistent storage. |
| **Instance Store-Backed AMI** | The root device for an instance launched from the AMI is an instance store volume created from a template stored in Amazon S3. | Suitable for temporary storage that changes frequently. |
| **Amazon Linux AMI** | A supported and maintained image provided by AWS, optimized for AWS platforms. | Ideal for applications that are designed to run on Amazon Linux. |
| **Windows AMI** | Provides Windows Server environments for running instances. | Used for applications that require Windows operating systems. |
| **Marketplace AMI** | AMIs provided by third-party vendors with pre-configured operating systems and software. | Useful for specialized software or licensing requirements. |
| **Community AMI** | AMIs that are created and shared by AWS users. | Good for community-supported configurations and applications. |
| **Private AMI** | Custom AMIs created by users for their own use, which can be shared with specific AWS accounts. | Best for customized environments that need to be replicated. |

For more detailed information on AWS AMIs, you can refer to the [AWS AMI documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html).

## EC2 pricing options

| Pricing Option | Description | Use Cases | Commitment | Savings Potential | Additional Points |
|----------------|-------------|-----------|------------|-------------------|-------------------|
| **On-Demand** | Pay for compute capacity by the hour or second with no long-term commitments. | Ideal for short-term, irregular workloads that cannot be interrupted. | None | None | Most flexible option, highest cost, instant availability. |
| **Reserved Instances** | Reserve instances for a 1 or 3-year term and get a significant discount over On-Demand rates. | Best for steady-state usage and applications with predictable usage. | 1 or 3 years | Up to 75% | Options for partial, all upfront, or no upfront payment. |
| **Savings Plans** | Commit to a consistent amount of usage (measured in $/hour) for a 1 or 3-year period and receive a lower rate. | Flexible usage across instance families and AWS regions. | 1 or 3 years | Up to 72% | Compute Savings Plans and EC2 Instance Savings Plans available. |
| **Spot Instances** | Purchase unused EC2 capacity at a steep discount. Instances can be interrupted by AWS with two minutes of notification. | Suitable for flexible start and end times, fault-tolerant applications, and data analysis. | None | Up to 90% | Best for workloads with flexible timing, significant cost savings. |
| **Dedicated Hosts** | Physical EC2 servers dedicated for your use which can help you meet compliance requirements. | Useful when you have server-bound software licenses that could complicate multi-tenant virtualization. | Per hour or reservation | Varies | Useful for regulatory or compliance needs, allows for existing license utilization. |
| **Dedicated Instances** | Instances run on hardware that's dedicated to a single customer. | When you need to ensure your instances are physically isolated at the host hardware level from instances that belong to other AWS accounts. | Per hour | Varies | Physical isolation meets certain compliance requirements. |
| **Capacity Reservations** | Reserve capacity for your EC2 instances in a specific Availability Zone for any duration. | When you need to ensure you have EC2 capacity when you need it, for as long as you need it. | None | Varies | Good for applications that require reserved capacity. |

## Detailed Amazon EC2 Instance Types Comparison

| Category | Instance Type | Suitable For | vCPUs | RAM | Storage | Network Performance | Additional Features |
|----------|---------------|--------------|-------|-----|---------|---------------------|---------------------|
| General Purpose | T2/T3/T4g, M5/M6g | Various workloads with balanced needs | Variable | Variable | EBS only | Up to 25 Gbps | Cost-effective, good for small to medium databases |
| Compute Optimized | C5/C6g | High-performance computing, batch processing | High | Moderate | EBS only | Up to 100 Gbps | High CPU performance, good for CPU-bound applications |
| Memory Optimized | R5/R6g | Large databases, memory-intensive applications | Moderate | High | EBS only | Up to 100 Gbps | Fast performance for large in-memory processing |
| Storage Optimized | I3/I3en | High frequency, I/O intensive apps, large databases | High | High | SSD/HDD | Up to 100 Gbps | High random I/O access, high sequential read/write |
| Accelerated Computing | P3/P4 | Machine learning, graphics-intensive applications | Variable | High | EBS only | Up to 100 Gbps | NVIDIA GPUs, high-performance computing |
| High Performance Computing | HPC6id | Scientific modeling, engineering applications | Very High | High | EBS only | Up to 400 Gbps | Low latency networking, high network throughput |

### Additional Considerations

- **Pricing**: Costs can vary significantly between instance types and sizes, and also depend on the chosen pricing model (On-Demand, Reserved, Spot Instances).
- **Scalability**: Some instance types offer auto-scaling features, allowing you to adjust resources based on demand.
- **Security**: All instance types can be launched within an Amazon VPC, providing a secure and isolated environment.
- **Flexibility**: With the option to change instance types and sizes, you can optimize costs and performance as your needs evolve.

## AWS Reserved Instances Types Comparison

| Feature | Standard Reserved Instance | Convertible Reserved Instance | Scheduled Reserved Instance |
|---------|----------------------------|-------------------------------|-----------------------------|
| **Discount Level** | Highest discount rates | Lower discount rates compared to Standard | Moderate discount rates |
| **Term Flexibility** | 1 or 3 years | 1 or 3 years | Customizable within the term |
| **Modification** | Limited modification options | More flexible modifications | Limited to the schedule |
| **Exchangeability** | Not exchangeable | Exchangeable for other Convertible Reserved Instances | Not exchangeable |
| **Marketplace** | Can be sold in the Reserved Instance Marketplace | Cannot be sold | Cannot be sold |
| **Capacity Reservation** | Guaranteed capacity reservation | Optional capacity reservation | Guaranteed capacity reservation for the scheduled time |
| **Use Case** | Best for stable workloads with predictable usage | Suitable for changing workloads or instance types | Ideal for workloads with a known schedule |

## AWS Security Services

### Comparison of AWS Security Services

AWS offers a variety of security services designed to help protect your applications and data. Below is a comparison of some of these services, including their primary use cases.

| Service | Description | Use Cases |
|---------|-------------|-----------|
| **AWS Identity and Access Management (IAM)** | Manages access to AWS services and resources securely. | User and group management, access policies, multi-factor authentication. |
| **AWS Key Management Service (KMS)** | Manages cryptographic keys for your applications. | Encryption and decryption of data, management of cryptographic keys. |
| **AWS WAF (Web Application Firewall)** | Protects web applications from common web exploits. | Filtering traffic, blocking common attack patterns, such as SQL injection or cross-site scripting. |
| **AWS Shield** | Provides protection against Distributed Denial of Service (DDoS) attacks. | Protecting applications running on AWS from DDoS attacks. |
| **Amazon Inspector** | Automated security assessment service to help improve the security and compliance of applications deployed on AWS. | Assessing applications for vulnerabilities or deviations from best practices. |
| **AWS Secrets Manager** | Protects access to your applications, services, and IT resources. | Managing secrets, rotating credentials automatically, secure application access. |
| **AWS Certificate Manager** | Provisions, manages, and deploys public and private SSL/TLS certificates. | Managing SSL/TLS certificates for AWS-based websites and applications. |
| **AWS CloudTrail** | Enables governance, compliance, operational auditing, and risk auditing of your AWS account. | Logging and monitoring account activity across your AWS infrastructure. |
| **Amazon GuardDuty** | Provides intelligent threat detection to protect your AWS accounts and workloads. | Monitoring for malicious or unauthorized behavior to protect your AWS accounts. |
| **AWS Cognito** | Provides user identity and data synchronization to help create a secure user directory. | User authentication and mobile data synchronization. |
| **AWS Security Hub** | Gives you a comprehensive view of your high-priority security alerts and compliance status. | Aggregating security findings from various services, automated compliance checks. |
| **AWS Audit Manager** | Helps you continuously audit your AWS usage to simplify how you manage risk and compliance with regulations and industry standards. | Automating evidence collection, simplifying compliance audits, and managing stakeholder reviews. |
| **AWS Macie** | A fully managed data security and data privacy service that uses machine learning and pattern matching to discover and protect sensitive data in AWS. | Discovering and protecting sensitive data in Amazon S3, monitoring data access for anomalies. |
| **AWS CloudHSM** | Offers secure cryptographic key storage by providing managed hardware security modules in the AWS Cloud. | Cryptographic key storage, FIPS 140-2 level 3 security, dedicated hardware security module management. |

For a more comprehensive understanding of AWS security services and how they can be applied to your specific use case, refer to the [AWS Security Services documentation](https://docs.aws.amazon.com/cloudhsm/).

## AWS Identity and Access Management (IAM)

AWS IAM is a web service that helps you securely control access to AWS resources. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.

### Key Features of AWS IAM

- **Fine-Grained Access Control**: Manage permissions and control access to AWS services and resources with precision.

- **Multi-Factor Authentication (MFA)**: Add an extra layer of security by enabling two-factor authentication for users.

- **Identity Federation**: Allow users to authenticate with IAM using their existing corporate credentials.

- **Roles and Policies**: Assign permissions to users, groups, and roles using policies written in JSON format.

- **Temporary Security Credentials**: Provide temporary access to your AWS resources by using roles and federated users.

- **Centralized Control**: Manage all user access and permissions from a single location within the AWS Management Console.

- **Shared Access to Your AWS Account**: Delegate access to your AWS resources without sharing your AWS account credentials.

- **Integrated with Many AWS Services**: Seamlessly integrated with other AWS services to control access to their resources.

- **Supports PCI DSS Compliance**: IAM supports the processing, storage, and transmission of credit card data by a merchant or service provider, and is compliant with the Payment Card Industry Data Security Standard (PCI DSS).

- **Customizable Password Policy**: Set custom password policies to manage password complexity and rotation requirements.

- **AWS IAM Access Analyzer**: Analyze resource policies to help you determine which policies provide public or cross-account access.

- **Service-Linked Roles**: Predefined roles that provide permissions for AWS services to access resources in other services on your behalf.

- **Access Advisor**: View the service permissions granted to a user and when those services were last accessed.

- **Policy Simulator**: Test and troubleshoot IAM and resource-based policies to ensure they grant the intended permissions.

- **AWS Organizations Integration**: Centrally manage policies across multiple AWS accounts.

## Comparison of AWS IAM Users, Groups, and Roles

| Feature | IAM Users | IAM Groups | IAM Roles |
|---------|-----------|------------|-----------|
| **Definition** | An IAM user is an entity that represents a person or application that interacts with AWS services. | An IAM group is a collection of IAM users that you can manage as a single unit. | An IAM role is an entity with permission policies that determine what the identity can and cannot do in AWS. |
| **Credentials** | Can be assigned long-term credentials like passwords and access keys. | Does not have credentials; instead, users within the group inherit permissions. | Does not have standard long-term credentials. Access is provided via temporary security tokens. |
| **Use Case** | For individuals or applications requiring long-term access to AWS resources. | To manage permissions for multiple users with similar responsibilities. | For delegating permissions across AWS services, accounts, or to federated users. |
| **Permissions** | Assigned directly to the user or inherited through group membership. | Permissions are assigned to the group, and all users within the group inherit them. | Assigned to the role and assumed by trusted entities. |
| **Best Practice** | Create individual IAM users for anyone who needs access to your AWS account. | Use groups to assign permissions to users with similar job functions. | Use roles for applications running on EC2 instances or for cross-account access. |

For more detailed information and best practices, you can refer to the official [AWS IAM documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_version.html).

## AWS Defense Layers of Security

AWS advocates for a comprehensive security strategy that involves multiple layers of defense to protect and manage resources effectively. This multi-layered approach is aligned with the AWS Well-Architected Framework.

### Expanded Defense Layers

| Layer | Description | AWS Services | Additional Points |
|-------|-------------|--------------|-------------------|
| **Edge of Network** | Protection against DDoS attacks and other external threats. | AWS Shield, Amazon CloudFront | Utilizes global edge locations to detect and mitigate threats before they reach your resources|
| **VPC** | Isolation of resources within a virtual network. | Amazon VPC, Security Groups, Network ACLs | Supports VPC peering and endpoints for secure interconnectivity|
| **Load Balancer** | Distribution of traffic across resources, providing an additional layer of security. | Elastic Load Balancing (ELB) | Offers SSL/TLS termination to help manage certificates and encryption. |
| **Compute** | Security at the instance or service level. | Amazon EC2, AWS Lambda | Includes instance identity and isolation, along with service-specific security features. |
| **Operating System** | Hardening of the OS and management of host-based firewalls. | Amazon EC2 instances, AWS Systems Manager | Regular patching and configuration management to maintain security posture. |
| **Application** | Security measures within the application code and runtime environment. | AWS WAF, Amazon Inspector | Real-time inspection and protection against web exploits and vulnerabilities. |
| **Data** | Encryption and access controls for data at rest and in transit. | Amazon S3, AWS Key Management Service (KMS) | Use of encryption keys managed by KMS and integration with AWS Identity and Access Management (IAM). |

## Best Practices

- **Apply Security at All Layers**: Implement security controls at every layer of your stack, from the edge to the data layer.
- **Automate Security Best Practices**: Use AWS services to automate security best practices, ensuring consistent application across resources.
- **Protect Data in Transit and at Rest**: Utilize AWS encryption services to secure data, regardless of its state.
- **Prepare for Security Events**: Implement an incident response plan and conduct regular simulations to ensure readiness.

For more detailed guidance on implementing these security layers, you can refer to the [AWS Security Blog](https://aws.amazon.com/blogs/security/security-at-multiple-layers-for-web-administered-apps/) and the [AWS Well-Architected Framework documentation](https://docs.aws.amazon.com/whitepapers/latest/security-at-the-edge/security-at-the-edge.pdf).

## AWS CloudFormation

AWS CloudFormation is an automated provisioning engine designed to deploy resources consistently and repeatably across various AWS services. It enables developers and system administrators to create and manage a collection of related AWS resources by provisioning and updating them in an orderly and predictable fashion.

### Key Benefits of AWS CloudFormation

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

## SQS vs SNS vs SES

| Feature | SQS (Simple Queue Service) | SNS (Simple Notification Service) | SES (Simple Email Service) |
|---------|----------------------------|----------------------------------|----------------------------|
| **Type** | Message queuing service | Pub/sub messaging service | Email sending service |
| **Use Case** | Decouples components of a distributed system | Sends messages to multiple subscribers | Sends transactional and marketing emails |
| **Delivery** | Messages are pulled by the receiver | Pushes messages to subscribers | Directly to email recipients |
| **Persistence** | Messages are stored until they're processed | No message storage for retrieval, but retains messages for a short period for delivery retries | No storage, emails are sent and then deleted |
| **Scalability** | Can handle a high number of messages | Supports a large number of subscribers | Designed for high-volume email delivery |
| **Reliability** | Guarantees delivery of each message at least once | Delivers messages to all active subscribers | High deliverability with content filtering |
| **Communication** | A2A (Application to Application) | A2A and A2P (Application to Person) | A2P |
| **Ordering** | Standard and FIFO (First-In-First-Out) queues | Standard topics for unordered, FIFO for ordered delivery | N/A |
| **Data Protection** | Encryption at rest, message retention policies | Data masking, encryption in transit, and at rest | Content filtering, dedicated IP addresses |

## AWS Machine Learning Services

AWS offers a comprehensive set of machine learning services catering to various needs, from data scientists to developers and business analysts. Below is a summary of some key services:

### Amazon SageMaker

- **Description**: A fully managed service that enables data scientists and developers to quickly build, train, and deploy machine learning models.
- **Key Features**:
  - End-to-end machine learning workflow
  - Broad framework support
  - One-click model deployment
  - Integrated Jupyter notebooks

### Amazon Rekognition

- **Description**: A service that makes it easy to add image and video analysis to your applications.
- **Key Features**:
  - Object and scene detection
  - Facial recognition and analysis
  - Unsafe content detection
  - Text in image recognition

### Amazon Comprehend

- **Description**: A natural language processing (NLP) service that uses machine learning to find insights and relationships in text.
- **Key Features**:
  - Sentiment analysis
  - Entity recognition
  - Key phrase extraction
  - Language detection

### Amazon Polly

- **Description**: A service that turns text into lifelike speech, allowing you to create applications that talk.
- **Key Features**:
  - Lifelike speech synthesis
  - Supports multiple languages and voices
  - Easy integration with other AWS services

### Amazon Lex

- **Description**: A service for building conversational interfaces into any application using voice and text.
- **Key Features**:
  - Automatic speech recognition (ASR)
  - Natural language understanding (NLU)
  - Integration with AWS Lambda for fulfilling functions

### Amazon Translate

- **Description**: A neural machine translation service that delivers fast, high-quality, and affordable language translation.
- **Key Features**:
  - Real-time translation
  - Support for multiple languages
  - Customizable translation

### Amazon Textract

- **Description**: A service that automatically extracts text and data from scanned documents.
- **Key Features**:
  - Extracts text, forms, and tables
  - Machine learning-based document analysis
  - Easy integration with other AWS services

## AWS Elastic Load Balancing (ELB)

AWS Elastic Load Balancing (ELB) automatically distributes incoming application traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in one or more Availability Zones. It ensures high availability and fault tolerance for your applications.

### Key Features

- **Automatic Distribution**: Distributes incoming traffic across multiple targets in different Availability Zones.
- **Health Checks**: Monitors the health of registered targets and routes traffic only to healthy ones.
- **Scalability**: Scales the load balancer capacity automatically in response to incoming traffic changes.
- **Types of Load Balancers**:
  - **Application Load Balancer**: Best suited for HTTP and HTTPS traffic, providing advanced request routing.
  - **Network Load Balancer**: Ideal for TCP, UDP, and TLS traffic where performance is required.
  - **Gateway Load Balancer**: Simplifies the deployment of third-party virtual appliances.
  - **Classic Load Balancer**: Provides basic load balancing across multiple EC2 instances.

## AWS Auto Scaling

AWS Auto Scaling ensures that you have the correct number of Amazon EC2 instances available to handle the load for your application. It can automatically increase or decrease resource capacity in response to changing demand.

### Auto-Scaling Key Features

- **Dynamic Scaling**: Adjusts the number of EC2 instances in response to real-time demand metrics.
- **Predictive Scaling**: Uses machine learning to schedule the right number of EC2 instances based on predicted demand.
- **Health Checks**: Automatically replaces instances that fail health checks.
- **Cost-Effective**: Reduces costs by terminating unnecessary instances and launching new ones when needed.
- **Integrated with AWS Services**: Works with services like EC2, ECS, RDS, and DynamoDB.

### How It Works

1. **Define Scaling Policies**: Set parameters based on desired, minimum, and maximum number of instances.
2. **Monitor Application Demand**: Use Amazon CloudWatch to monitor traffic and trigger scaling actions.
3. **Automatic Scaling**: Instances are automatically added or removed according to policies and demand.

### Benefits

- **Improved Availability**: Maintains application performance during demand spikes.
- **Cost Savings**: Only use and pay for the resources you need.
- **Time-Saving**: Automates the scaling process, freeing up time for other tasks.

## AWS Route 53

AWS Route 53 is a scalable and highly available Domain Name System (DNS) web service. It is designed to give developers and businesses an extremely reliable and cost-effective way to route end users to Internet applications.

### Route 53 Key Features

- **DNS Service**: Route 53 translates friendly domain names like www.example.com into IP addresses like 192.0.2.1.
- **Health Checking**: Automatically sends requests to endpoints to verify they are reachable, available, and functional.
- **Traffic Flow**: Manages traffic globally through a variety of routing types, including latency-based routing, Geo DNS, and Weighted Round Robin—all of which can be combined with DNS Failover to enable a variety of low-latency, fault-tolerant architectures.
- **Domain Registration**: Helps you purchase and manage domain names such as .com, .net, and .org.
- **SSL Certificate Management**: Integrates with AWS Certificate Manager for easy management and deployment of SSL/TLS certificates.
- **Private DNS for Amazon VPC**: Manages custom domain names for your AWS resources using private DNS within your Virtual Private Cloud (VPC).

### Use Cases

- **Web Application Hosting**: Reliable and cost-effective way to route visitors to your web applications.
- **Global Server Load Balancing**: Route traffic to multiple endpoints worldwide, which can be in AWS or outside of AWS.
- **Disaster Recovery**: Set up DNS health checks and failover to reroute your users to a standby web environment in case your primary web application becomes unavailable.

## AWS CloudWatch vs CloudTrail

AWS CloudWatch is focused on the operational aspects, such as performance and health of AWS services, while CloudTrail is focused on the compliance and governance aspects, tracking the API calls and activities within your AWS account

| Feature | AWS CloudWatch | AWS CloudTrail |
|---------|----------------|----------------|
| **Purpose** | Monitors AWS resources and applications, providing operational data and insights. | Records AWS account activity, providing logs for security and compliance auditing. |
| **Primary Use** | Real-time monitoring of metrics and logs for performance and health of AWS services. | Tracking user activity and API usage to ensure governance and compliance. |
| **Data Provided** | Metrics, logs, alarms, and events related to AWS resources and applications. | API call history, including who made the call, from where, and when. |
| **Functionality** | Offers dashboards, alarms, and insights for resource optimization. | Provides event history for auditing and operational troubleshooting. |
| **Integration** | Integrates with AWS services for monitoring and operational management. | Integrates with AWS services for governance, compliance, and risk auditing. |
| **Data Availability** | Metric data is available in 1-minute periods for detailed monitoring. | Event data is delivered within 15 minutes of the API call. |
| **Storage** | Stores data in CloudWatch dashboards as metrics and logs. | Centralizes logs across regions/accounts and stores them in S3 buckets. |
| **Pricing** | Free basic monitoring; charges apply for detailed monitoring and additional features. | Free for basic event history; charges apply for extended history and log delivery to S3. |
| **Common Users** | Developers, IT operators, and system administrators. | Security and compliance teams, auditors, and IT administrators. |

## AWS Organizations

AWS Organizations is an AWS service designed for account management, enabling you to consolidate multiple AWS accounts into a single organization.

### Core Features

- **Account Management**: Centralize control over your AWS accounts, making it easier to manage them as a cohesive unit.
- **Consolidated Billing**: Receive a single bill for all accounts within your organization, simplifying the payment process.
- **Organizational Units (OUs)**: Structure your accounts into OUs for finer-grained control over resources and policies.
- **Service Control Policies (SCPs)**: Apply permission policies across your organization to ensure compliance and security.

### Advanced Features

- **Tag Policies**: Implement standard tags across your organization for consistent resource identification.
- **Backup Policies**: Automate AWS Backups across multiple accounts for enhanced data protection.
- **AI Services Opt-Out Policies**: Control the use of AI services that store customer content.

### Best Practices

- **Use OUs for Scalability**: As your organization grows, use OUs to manage accounts more effectively.
- **Implement Strong SCPs**: Ensure that SCPs are robust and reflect your organization's security requirements.
- **Monitor with AWS CloudTrail**: Keep track of user activity and API usage across your AWS accounts.

### Getting Started

1. **Create Your Organization**: Set up your organization and designate a management account.
2. **Invite Accounts**: Add existing AWS accounts or create new ones within your organization.
3. **Set Up OUs**: Organize your accounts into OUs and assign relevant policies.
4. **Apply SCPs**: Define and apply SCPs to manage permissions and maintain security standards.

![alt text](image-3.png)
<https://docs.aws.amazon.com/organizations/latest/userguide/orgs_getting-started_concepts.html>

## AWS Well-Architected Framework

The AWS Well-Architected Framework is a guide for building and operating secure, efficient, and resilient systems in the cloud. It provides a set of best practices and a consistent approach for evaluating architectures.

### The Five Pillars of the AWS Well-Architected Framework

1. **Operational Excellence**: Focuses on running and monitoring systems to deliver business value and continually improving processes and procedures.
2. **Security**: Concentrates on protecting information and systems, ensuring confidentiality and integrity of data, and establishing controls to detect security events.
3. **Reliability**: Ensures that workloads perform their intended functions correctly and consistently over time.
4. **Performance Efficiency**: Looks at how to use computing resources efficiently to meet system requirements and maintain that efficiency as demand changes and technologies evolve.
5. **Cost Optimization**: Involves understanding and controlling where money is being spent, selecting the most appropriate and right number of resource types, and scaling to meet business needs without overspending.

### Additional Points

- **Sustainability Pillar**: Recently added to help you build and operate workloads that are environmentally friendly.
- **Well-Architected Tool**: A service provided by AWS to review and measure your architecture against best practices.
- **Well-Architected Labs**: Provides hands-on labs to help you learn how to implement best practices and measure your workloads.
- **Well-Architected Reviews**: Periodic reviews recommended to ensure that workloads remain aligned with best practices as they evolve.

### Best Practices and Design Principles

- **Automate Everything**: Automation can help make architectural experimentation easier, and operational problems more predictable to manage.
- **Document Everything**: Keep thorough documentation to ensure that everyone has the same understanding of how systems are designed and managed.
- **Make Frequent, Small, Reversible Changes**: This approach helps to minimize the scope of any one change and increases the overall agility of the team.

## AWS Cloud Adoption Framework (CAF)

The AWS Cloud Adoption Framework (CAF) is a blueprint for cloud adoption that provides best practices and guidance to support your organization throughout the cloud adoption journey.

### Six Perspectives of AWS CAF

#### Business Perspective

- **Focus**: Aligns IT strategy with business goals.
- **Key Activities**: Define business outcomes, identify stakeholders, establish governance models.
- **Benefits**: Ensures cloud initiatives drive desired business outcomes.

#### People Perspective

- **Focus**: Supports human resources and staffing strategies that adapt to cloud-based operating models.
- **Key Activities**: Develop talent, create new roles, and adjust organizational structures.
- **Benefits**: Builds a cloud-savvy workforce ready to deliver on cloud capabilities.

#### Governance Perspective

- **Focus**: Helps align IT governance with organizational governance.
- **Key Activities**: Implement best practices for budgeting, cost management, and asset compliance.
- **Benefits**: Provides a framework for making consistent and informed decisions.

#### Platform Perspective

- **Focus**: Ensures the implementation of efficient and effective technology platforms.
- **Key Activities**: Select appropriate technologies, optimize for the cloud, and manage architecture.
- **Benefits**: Delivers a robust and secure platform for cloud services.

#### Security Perspective

- **Focus**: Protects information and systems by ensuring confidentiality, integrity, and availability.
- **Key Activities**: Define security policies, manage data protection, and establish risk management protocols.
- **Benefits**: Enhances the security posture and compliance of cloud workloads.

#### Operations Perspective

- **Focus**: Manages and automates operations to deliver continuous value.
- **Key Activities**: Implement monitoring, incident response, and process optimization.
- **Benefits**: Increases operational efficiency and system reliability.

### CAF Additional Points

- **CAF Alignment**: Aligns cloud strategy with the AWS Well-Architected Framework.
- **CAF Resources**: Offers tools like the AWS CAF Alignment Tool to assess cloud readiness.
- **Continuous Improvement**: Encourages iterative improvement of cloud practices.

## Amazon CloudFront

Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds.

### How CloudFront Works

- **Content Delivery**: CloudFront delivers your content through a worldwide network of data centers called edge locations.
- **Low Latency**: When a user requests content, the request is routed to the edge location that provides the lowest latency.
- **Origin Sources**: CloudFront retrieves content from an origin you've defined, such as an Amazon S3 bucket or an HTTP server.

### Amazon CloudFront Key Features

- **Global Distribution**: Utilizes a global network of edge locations to cache and deliver content.
- **Security**: Integrates with AWS Shield for DDoS protection and AWS Web Application Firewall (WAF) for a robust security layer.
- **Customizability**: Offers a variety of features to customize content delivery, including URL signing, SSL/TLS encryption, and more.

### Amazon CloudFront Use Cases

- **Static and Dynamic Content Delivery**: Efficiently distributes both static (.html, .css, .js) and dynamic content.
- **Video Streaming**: Optimizes the delivery of video content with high data transfer rates.
- **Software Distribution**: Delivers software and updates to users around the world.

## AWS Trusted Advisor

AWS Trusted Advisor is an online resource that helps you optimize your AWS environment for cost, performance, security, and more by providing best practice recommendations.

### Core Benefits

- **Align with AWS Best Practices**: Identify deviations and get recommended actions to remediate.
- **Prioritize Important Recommendations**: Focus on the most critical recommendations based on your business priorities and urgency.
- **Streamline Collaboration**: Improve alignment across teams with better visibility and tracking of recommendations.
- **Optimize Resources at Scale**: View aggregated recommendations across your organization or integrate programmatically with APIs.

### Trusted Advisor Key Features

- **Cost Optimization**: Identifies underutilized resources to reduce costs and advises on Reserved Instance purchases.
- **Performance Improvement**: Analyzes usage and configuration to improve application speed and responsiveness.
- **Security Assessment**: Checks against security standards and best practices to address gaps.
- **Resilience Enhancement**: Examines the environment for redundancy shortfalls and suggests improvements.
- **Service Limits Tracking**: Monitors usage and notifies when approaching or exceeding service limits.

## Access and Support Plans

- **Basic and Developer Support Plans**: Limited access to checks.
- **Business and Enterprise Support Plans**: Full access to all checks, Trusted Advisor Priority, and API access.

## AWS Systems Manager

AWS Systems Manager enables visibility and control of your infrastructure on AWS. It provides a unified interface that allows you to automate operational tasks and manage your AWS resources.

### AWS Systems Manager:Key Features

| Feature | Description |
|---------|-------------|
| **Centralized Control** | Manage your AWS resources centrally. |
| **Visibility into Systems** | Get operational insights about the health and performance of your infrastructure. |
| **Automation** | Automate operational tasks to increase efficiency and reduce human error. |
| **Change Management** | Automate change requests and approvals, ensuring standardized operational procedures. |
| **Operational Insights** | Use CloudWatch and CloudTrail integration for detailed logging and monitoring. |
| **Hybrid Environment Management** | Manage both AWS and on-premises resources with a single interface. |
| **Compliance Enforcement** | Ensure your resources are compliant with policy requirements. |

### Additional Capabilities

| Capability | Description |
|------------|-------------|
| **Resource Groups** | Organize resources based on tags and manage them collectively. |
| **Insights Dashboard** | View aggregated data and act on operational issues. |
| **Parameter Store** | Securely store configuration data and secrets. |
| **Automation** | Simplify common maintenance and deployment tasks. |
| **Patch Manager** | Automate patching of your EC2 instances and on-premises servers. |
| **State Manager** | Maintain consistent configuration of your instances. |
| **Inventory Management** | Collect software inventory and use it for operational tasks and compliance. |
| **Maintenance Windows** | Schedule maintenance windows for performing potentially disruptive actions. |
| **Document Builder** | Use Document Builder to create runbooks with automation actions without needing JSON or YAML syntax. |