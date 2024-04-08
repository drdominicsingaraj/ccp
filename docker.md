# Docker

Docker is a platform that enables developers to build, run, manage, and distribute applications by using containers. Containers allow you to package an application with all of its dependencies into a standardized unit for software development.

## Amazon ECR (Elastic Container Registry)

Amazon ECR is a fully managed Docker container registry provided by AWS. It allows developers to store, manage, and deploy Docker container images. It's integrated with Amazon ECS and EKS, simplifying your development to production workflow.

## Amazon ECS (Elastic Container Service)

Amazon ECS is a fully managed container orchestration service provided by AWS. It allows you to run, manage, and scale containerized applications using Docker containers. ECS can be used with AWS Fargate, which is a serverless compute engine that removes the need to provision and manage servers.

## Amazon EKS (Elastic Kubernetes Service)

Amazon EKS is a managed service that makes it easier to run Kubernetes on AWS without needing to install, operate, and maintain your own Kubernetes control plane. It automates the deployment, scaling, and management of containerized applications and integrates with AWS services for secure networking, monitoring, and scaling.

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
