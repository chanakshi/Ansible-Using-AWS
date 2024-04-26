# Ansible AWS Setup for Installing .NET on EC2 Instances

This repository contains Ansible playbooks and configurations for managing EC2 instances on AWS and installing .NET on two guest user instances.

## Overview

This setup utilizes Ansible to automate the provisioning and configuration of EC2 instances on AWS and install .NET on them. It follows these key steps:

1. **AWS EC2 Setup**: Ansible is used to launch and manage EC2 instances on AWS.
2. **.NET Installation**: Ansible playbook is used to install .NET on the EC2 instances.
3. **Verification**: After installation, verify that .NET is correctly installed on the instances.

## Prerequisites

Before running the Ansible playbooks, ensure you have the following:

- An AWS account with the necessary permissions to create and manage EC2 instances.
- Ansible installed on your local machine.
- AWS CLI configured with credentials.
- SSH private key (.pem file) to access the EC2 instances.

## Setup Instructions

1. **Clone the Repository**:
   ```bash
   git clone <repository-url>
   cd ansible-aws-dotnet
   ```

2. **Configure AWS Credentials**:
   - Make sure your AWS credentials are correctly configured on your local machine. You can do this by running `aws configure` and entering your AWS Access Key ID and Secret Access Key.

3. **Update the Inventory File**:
   - Open the `inventory.ini` file and replace `<ec2-instance-1-ip>` and `<ec2-instance-2-ip>` with the public IP addresses of your EC2 instances.

4. **Update Ansible Hosts File**:
   - Open the `/etc/ansible/hosts` file on your local machine with a text editor.
   - Add the public IP addresses of your EC2 instances under appropriate groups. For example:
     ```
     [ec2]
     <ec2-instance-1-ip>
     <ec2-instance-2-ip>
     ```

5. **Copy SSH Private Key (.pem)**:
   - Copy the SSH private key (.pem file) to the directory where you are running the Ansible playbook.
   - Ensure that the permissions on the .pem file are restricted to read-only for the owner:
     ```bash
     chmod 400 your-key.pem
     ```

6. **Review and Customize the Playbook**:
   - Open the `playbook.yml` file and review the tasks.
   - Customize any variables or tasks as per your requirements.

7. **Run the Playbook**:
   ```bash
   ansible-playbook -i inventory.ini playbook.yml --private-key=your-key.pem
   ```

8. **Verification**:
   - After the playbook execution completes, SSH into each EC2 instance using the .pem file:
     ```bash
     ssh -i your-key.pem ec2-user@
     ```
