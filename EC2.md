# Elastic Compute Cloud

What are the different ways to connect to an Amazon EC2 instance?

**EC2 Instance Connect**: Provides a secure way of connecting to your Linux instances using SSH directly from the AWS Management Console or the EC2 Instance Connect CLI. It pushes a one-time-use SSH public key to the instance metadata for 60 seconds for enhanced security.

**Session Manager**: Part of AWS Systems Manager, it allows you to manage your EC2 instances through an interactive shell or through the AWS CLI without opening inbound ports or managing SSH keys. It provides a secure connection tunneled over a proxy connection, and the session manager agent establishes a reverse connection to the service.

**SSH client**: A traditional method of accessing remote servers, which requires network connectivity, user credentials, and often the management of SSH keys. It’s a protocol that provides a secure channel over an unsecured network in a client-server architecture.

**Remote Desktop Protocol (RDP)**: For Windows instances, you can use an RDP client to connect to your instance using its public DNS name or IP address.

**EC2 serial console**: Allows you to troubleshoot boot and network connectivity issues by providing access to the serial port of the instance. This can be particularly useful when you cannot connect to your instance using SSH1.
Each method has its own use cases and benefits, and the choice depends on the specific needs and security requirements of your AWS environment.