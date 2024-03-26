## Issue 1

**Problem:**
Encountered issues while running the `terraform init` command in the local machine's terminal.

![alt text](image.png)

**Solution:**

There were issues fetching latest AMI Id due to Indentation issues in the terraform configuration file. Fixing this issue helped fetching right AMI id, consequently EC2 launch worked fine. Please note that this is not an issue with the terraform installation issue.

### Select the newest AMI

![alt text](image-1.png)

**Terraform `fmt`** is used to standardize the format and style of your Terraform configuration files.

When you run `terraform fmt`, it rewrites your Terraform configuration files to a canonical format and style. It applies a subset of the Terraform language style conventions, along with other minor adjustments for readability. The formatting decisions are intentionally opinionated and have no customization options because the goal is to encourage consistency.

Consistent formatting makes it easier for developers to collaborate and maintain code. Other Terraform commands that generate configuration files will produce files that conform to the style imposed by `terraform fmt`. Adopting this style in your own files ensures consistency.

**Usage:**
You can use `terraform fmt` with the following options:
- `-list=false`: Don't list files containing formatting inconsistencies.
- `-write=false`: Don't overwrite input files (implied by `-check` or when input is STDIN).
- `-diff`: Display diffs of formatting changes.
- `-check`: Check if the input is formatted. Exit status will be 0 if all input is properly formatted.

By default, it scans the current directory for configuration files. You can specify a target directory or file.

**Example of `terraform fmt -diff` Output:**

The `terraform fmt` command is used to rewrite Terraform configuration files to a canonical format and style. When you use the `-diff` option with this command, it displays the differences between the original and formatted code.

Here's an example of how you might use the `terraform fmt` command with the `-diff` option:

`terraform fmt -diff`

This command will show you a side-by-side comparison of the original code and the formatted code, highlighting the changes made by the formatter.

For instance, if you had a configuration file with the following content:

![alt text](image-2.png)

The - indicates lines that will be removed, and the + indicates lines that will be added, showing you exactly how the indentation and alignment will change to match the canonical format.

## Issue 2

Amazon VPC Peering Network Connectivity Issues

[![Amazon VPC Peering Network Connectivity Issues](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DDLB2yNDyFmM)](https://www.youtube.com/watch?v=DLB2yNDyFmM)