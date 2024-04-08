# Docker

Docker is a platform that enables developers to build, run, manage, and distribute applications by using containers. Containers allow you to package an application with all of its dependencies into a standardized unit for software development.

## Docker Installation

```markdown
To install Docker on an Amazon EC2 instance with the Amazon Linux AMI, follow these steps:
```

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
___

## Custom Docker Image

### Creating a Custom Docker Image with NGINX

Follow these steps to create a custom Docker image with NGINX:

#### Step 1: Create a Directory

Make a new directory for your project and navigate into it:

```bash
mkdir my-nginx-project
cd my-nginx-project
```

#### Step 2: Create an index.html

This will be your custom webpage displayed by NGINX.

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Custom NGINX</title>
</head>
<body>
    <h1>Welcome to My Custom NGINX Page!</h1>
</body>
</html>
```

Save this as `index.html` in your project directory.

#### Step 3: Write the Dockerfile

Create a Dockerfile with the following content:

```dockerfile
# Use the official NGINX image as a parent image
FROM nginx:latest

# Copy the index.html file from your local directory to the container
COPY index.html /usr/share/nginx/html/index.html

# Expose port 80
EXPOSE 80

# Start NGINX when the container launches
CMD ["nginx", "-g", "daemon off;"]
```

#### Step 4: Build Your Docker Image

Run the following command in your project directory to build the Docker image:

```bash
docker build -t my-custom-nginx .
```

#### Step 5: Run Your Container

Start a container using your new image:

```bash
docker run --name my-nginx-container -d -p 8080:80 my-custom-nginx
```

#### Step 6: Verify Your Deployment

Open a web browser and navigate to `http://localhost:8080` to see your custom NGINX page.

Remember to replace `my-custom-nginx` with the name you want for your Docker image and `my-nginx-container` with the name you want for your container.

## DockerHub Repository Overview

DockerHub is a service provided by Docker that serves as the world's largest container registry. Here's what you can do with DockerHub:

### Find and Pull Images

- Access a vast library of community and official images for your projects.

### Push and Store Images

- Upload your custom images for easy distribution and version control.

### Automated Builds

- Connect to GitHub or Bitbucket for automated image builds with code changes.

### Webhooks and Integration

- Set up webhooks for triggering actions in other services when an image is pushed.

## Pushing a Docker Image to DockerHub

Here's how you can push a Docker image to your DockerHub repository:

### Step 1: Log in to DockerHub

Log in to DockerHub via the command line:

```bash
docker login --username your-username
```

You'll be prompted to enter your password.

### Step 2: Tag Your Image

Tag your local image with your DockerHub username and the repository:

```bash
docker tag local-image:tag your-username/repository:tag
```

Replace `local-image:tag` with the name of your image and `your-username/repository:tag` with your DockerHub username and repository.

### Step 3: Push the Image

Push the image to DockerHub using the tag you've created:

```bash
docker push your-username/repository:tag
```

Replace `your-username/repository:tag` with your DockerHub username and repository.

Remember to replace `your-username`, `repository`, and `tag` with your actual DockerHub username, the name of your repository, and the tag of your image.

## Amazon ECR (Elastic Container Registry)

Amazon ECR is a fully managed Docker container registry provided by AWS. It allows developers to store, manage, and deploy Docker container images. It's integrated with Amazon ECS and EKS, simplifying your development to production workflow.

### Pushing a Docker Image to Amazon ECR

To push a Docker image to Amazon ECR, follow these steps:

### Step 1: Create an ECR Repository

Ensure you have an ECR repository to push your image to. If not, create one.

### Step 2: Authenticate Your Docker Client

Authenticate your Docker client to the Amazon ECR registry with the following command:

```bash
aws ecr get-login-password --region your-region | docker login --username AWS --password-stdin your-aws-account-id.dkr.ecr.your-region.amazonaws.com
```

Replace `your-region` and `your-aws-account-id` with your specific AWS region and account ID.

### Step 3: Tag Your Docker Image

Tag your local Docker image with the ECR repository URI:

```bash
docker tag local-image:tag your-aws-account-id.dkr.ecr.your-region.amazonaws.com/repository:tag
```

### Step 4: Push the Image to ECR

Push the tagged image to your ECR repository:

```bash
docker push your-aws-account-id.dkr.ecr.your-region.amazonaws.com/repository:tag
```

Replace `local-image:tag` with your image's name and tag, and `repository:tag` with your ECR repository's name and desired image tag.

For more detailed instructions, refer to the [Amazon ECR documentation](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html).

Please replace `your-region`, `your-aws-account-id`, `local-image:tag`, and `repository:tag` with your actual AWS region, AWS account ID, local Docker image name and tag, and ECR repository name and tag, respectively.

## Amazon Elastic Container Service (Amazon ECS)

Amazon ECS is a fully managed container orchestration service that allows you to deploy, manage, and scale containerized applications. Here are its key features:

### Fully Managed Service
ECS eliminates the need to install and operate your own cluster management infrastructure.

### Container Orchestration
Handles the deployment, scaling, and management of containers.

### Integration
Works seamlessly with AWS services like Elastic Load Balancing, Amazon RDS, and Amazon EC2.

### Capacity Providers
Manages the infrastructure to run containers, with options for both serverless (AWS Fargate) and EC2 instances.

### Scheduling
Allows you to place containers based on your resource needs and availability requirements.

### Security
Integrates with AWS Identity and Access Management (IAM) for resource-level control and security.

### Flexibility
Run tasks and services on a serverless infrastructure or on EC2 instances that you manage.

### ECS Anywhere
Run ECS in your own data center, providing flexibility to run applications on-premises or in the cloud.

ECS is designed to work well with Docker containers, making it easier for teams to focus on building their applications rather than managing the underlying infrastructure.

For more detailed information, refer to the official AWS documentation.

## ECS Implementation

Implementing Amazon ECS (Elastic Container Service) typically involves setting up a cluster, defining tasks and services, and then running and managing your containers within that environment. Here’s a high-level example of how you might set up a basic ECS deployment:

**Create an ECS Cluster**: This is where your container instances will live. You can create a cluster using the AWS Management Console or the AWS CLI.

**Define a Task Definition**: This is a blueprint for your application that describes the container and includes information like the image to use, CPU and memory allocations, environment variables, and port mappings.

**Launch and Register Container Instances**: These are the EC2 instances that run the container agent and will be part of your ECS Cluster.

**Create a Service**: This allows you to run and maintain a specified number of instances of a task definition simultaneously in an ECS cluster.

**Run Tasks**: This launches your containers based on the Task Definition within your cluster.
Update Services: If you need to update your application, you can create a new task definition and update the service to use it.

**Monitor Your Services**: Use Amazon CloudWatch to monitor the resource utilization of your services.
Here’s a simple example using the AWS CLI:

### Step 1: Create an ECS Cluster

```bash
aws ecs create-cluster --cluster-name my-cluster
```

### Step 2: Register a Task Definition

```bash
aws ecs register-task-definition --family my-task --container-definitions file://my-container-definition.json
```

### Step 3: Launch and Register Container Instances

### This step is automatically handled if you're using Fargate.

### Step 4: Create a Service

```bash
aws ecs create-service --cluster my-cluster --service-name my-service --task-definition my-task --desired-count 2
```

### Step 5: Run Tasks

```bash
aws ecs run-task --cluster my-cluster --task-definition my-task
```

#### Step 6: Update Services

```bash
aws ecs update-service --cluster my-cluster --service-name my-service --task-definition new-task-definition
```

#### Step 7: Monitor Your Services

#### Use Amazon CloudWatch from the AWS Management Console or AWS CLI

Remember to replace placeholder values like my-cluster, my-task, my-container-definition.json, and my-service with your actual ECS cluster name, task definitions, container definition files, and service names.

## Website setup using Amazon ECS

Setting up a website with Amazon ECS involves several steps, including creating a Docker image, pushing it to a registry, and then deploying it to ECS. Here's a simplified example using the AWS CLI and Docker:

1. **Create a Docker Image for Your Website**:
   - Write a `Dockerfile` for your website.
   - Build your Docker image: `docker build -t my-website .`

2. **Push the Image to Amazon ECR**:
   - Authenticate Docker to your ECR registry: `aws ecr get-login-password --region your-region | docker login --username AWS --password-stdin your-account-id.dkr.ecr.your-region.amazonaws.com`
   - Tag your image: `docker tag my-website:latest your-account-id.dkr.ecr.your-region.amazonaws.com/my-website:latest`
   - Push the image: `docker push your-account-id.dkr.ecr.your-region.amazonaws.com/my-website:latest`

3. **Create an ECS Cluster**:
   - Use the AWS CLI: `aws ecs create-cluster --cluster-name my-cluster`

4. **Create a Task Definition**:
   - Define the task with the necessary details like the image to use, CPU and memory requirements, etc.

5. **Create a Service**:
   - Create a service that runs and maintains a specified number of instances of your task definition: 
   `aws ecs create-service --cluster my-cluster --service-name my-website-service --task-definition my-website-task --desired-count 1 --launch-type FARGATE`

6. **Configure a Load Balancer**:
   - Set up an Application Load Balancer (ALB) to distribute traffic to your containers.

7. **Test Your Deployment**:
   - Once everything is set up, access your website via the ALB's DNS name.

Remember to replace placeholder values like `my-website`, `your-region`, `your-account-id`, `my-cluster`, `my-website-service`, and `my-website-task` with your actual Docker image name, AWS region, AWS account ID, ECS cluster name, service name, and task definition, respectively. The AWS CDK (Cloud Development Kit) can also be used to define your cloud infrastructure in a programming language you are familiar with, which simplifies the process of deploying your website on ECS.

## Amazon EKS (Elastic Kubernetes Service)

Amazon EKS is a managed service that makes it easier to run Kubernetes on AWS without needing to install, operate, and maintain your own Kubernetes control plane. It automates the deployment, scaling, and management of containerized applications and integrates with AWS services for secure networking, monitoring, and scaling.
