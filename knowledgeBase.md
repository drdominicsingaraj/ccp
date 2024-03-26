## Issue 1

**Problem:**
Encountered issues while running the `terraform init` command in the local machine's terminal.

![alt text](image.png)

**Solution:**

There were issues fetching latest AMI Id due to Indentation issues in the terraform configuration file. Fixing this issue helped fetching right AMI id, consequently EC2 launch worked fine. Please note that this is not an issue with the terraform installation issue.

### Select the newest AMI

![alt text](image-1.png)
