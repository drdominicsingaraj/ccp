# Docker

Docker is a platform that enables developers to build, run, manage, and distribute applications by using containers. Containers allow you to package an application with all of its dependencies into a standardized unit for software development.

## Amazon ECR (Elastic Container Registry)

Amazon ECR is a fully managed Docker container registry provided by AWS. It allows developers to store, manage, and deploy Docker container images. It's integrated with Amazon ECS and EKS, simplifying your development to production workflow.

## Amazon ECS (Elastic Container Service)

Amazon ECS is a fully managed container orchestration service provided by AWS. It allows you to run, manage, and scale containerized applications using Docker containers. ECS can be used with AWS Fargate, which is a serverless compute engine that removes the need to provision and manage servers.

## Amazon EKS (Elastic Kubernetes Service)

Amazon EKS is a managed service that makes it easier to run Kubernetes on AWS without needing to install, operate, and maintain your own Kubernetes control plane. It automates the deployment, scaling, and management of containerized applications and integrates with AWS services for secure networking, monitoring, and scaling.

Certainly! Here's the markdown code for the instructions on installing Docker on an Amazon EC2 instance with the Amazon Linux AMI:

```markdown
To install Docker on an Amazon EC2 instance with the Amazon Linux AMI, follow these steps:

1. **Connect to your EC2 instance using SSH:**

   ```bash
   ssh ec2-user@<your-ec2-ip-address>
   ```

2. **Update the installed packages and package cache on your instance:**

   ```bash
   sudo yum update -y
   ```

3. **Install Docker:**

   ```bash
   sudo yum install docker -y
   ```

4. **Start the Docker service:**

   ```bash
   sudo service docker start
   ```

5. **Add the `ec2-user` to the Docker group to execute Docker commands without using `sudo`:**

   ```bash
   sudo usermod -a -G docker ec2-user
   ```

6. **Log out and log back in again to pick up the new Docker group permissions.**

7. **(Optional) Install `docker-compose` using `pip`:**

   ```bash
   sudo yum install python3-pip
   pip3 install --user docker-compose
   ```

8. **Enable the Docker service to start on boot:**

   ```bash
   sudo systemctl enable docker.service
   ```

After these steps, Docker should be installed and running on your EC2 instance. You can verify the installation by checking the Docker service status:

```bash
sudo systemctl status docker.service
```
