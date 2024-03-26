## Issue 1

**Problem:**
Encountered issues while running the `terraform init` command in the local machine's terminal.

![alt text](image.png)

**Solution:**

There were issues fetching latest AMI Id due to Indentation issues in the terraform configuration file.

### Select the newest AMI

data "aws_ami" "latest_linux_ami" {
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["al2023-ami-2023*x86_64"]
  }
}
