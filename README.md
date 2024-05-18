# Ansible Playbook with Roles

This repository contains Ansible playbooks and Terraform configurations for deploying infrastructure and applications on AWS EC2 instances with Roles.

## Directory Structure

- **ansible-playbook-roles**: Directory containing Ansible playbook with roles.
    - **terraform-ec2**: Directory containing Terraform configuration for provisioning AWS EC2 instances.
        - **main.tf**: Terraform configuration file defining AWS resources like VPC, subnets, security groups, and EC2 instances.
        - **terraform.tfvars**: Terraform variables file containing configuration parameters such as VPC CIDR block, subnet CIDR block, etc.
    - **roles**: Directory containing Ansible roles.
        - **create_user**: Ansible role to create a new user on the EC2 instances.
            - **defaults**: Directory containing default variables.
                - **main.yaml**: Default user groups for the new user.
            - **tasks**: Directory containing tasks for creating a new user.
                - **main.yaml**: Task to create a new user.
            - **vars**: Directory containing role-specific variables.
                - **main.yaml**: Variable defining user groups for the new user.
        - **install_prerequisites**: Ansible role to install Docker and prerequisites.
            - **tasks**: Directory containing tasks for installing Docker and prerequisites.
                - **main.yaml**: Tasks to install Docker, Docker Compose, and manage packages.
            - **vars**: Directory containing role-specific variables.
                - **main.yaml**: Variable defining Docker Compose URL.
        - **start_docker_containers**: Ansible role to start Docker containers.
            - **defaults**: Directory containing default variables.
                - **main.yaml**: Default Docker registry URL, username, and password.
            - **files**: Directory containing files related to Docker containers.
                - **docker-compose.yaml**: Docker Compose configuration for services.
            - **tasks**: Directory containing tasks for starting Docker containers.
                - **main.yaml**: Tasks to copy Docker Compose file and start Docker containers.
            - **vars**: Directory containing role-specific variables.
                - **main.yaml**: Variable defining Docker registry URL, username, and password.
    - **ansible.cfg**: Ansible configuration file specifying settings like inventory and remote user.
    - **deploy-docker.yaml**: Ansible playbook for deploying Docker containers.
    - **inventory_aws_ec2.yaml**: Ansible inventory file for AWS EC2 instances.
    - **manual-installation.sh**: Shell script for manual installation of Docker and Docker Compose.

## Usage

1. **Terraform Configuration**:
   - Navigate to the `terraform-ec2` directory.
   - Update the `terraform.tfvars` file with desired configurations.
   - Run `terraform init`, `terraform plan`, and `terraform apply` to provision EC2 instance(s) on AWS.

2. **Ansible Configuration**:
   - Update `ansible.cfg` with necessary settings.
   - Ensure that the inventory file `inventory_aws_ec2.yaml` contains correct AWS EC2 instance information.
   - Adjust the playbook `deploy-docker.yaml` and role variables files if needed for custom configurations.

3. **Deploy Docker Containers**:
   - Execute the Ansible playbook `deploy-docker.yaml` to start Docker containers on the provisioned EC2 instance(s).
   - Verify the deployment by accessing the deployed services.

4. **Manual Installation (Optional)**:
   - If needed, you can use `manual-installation-docker.sh` for manual Docker installation on servers.

## Notes
- This setup automates the deployment of Docker containers on AWS EC2 instances using Ansible and Terraform.
- Customize the Terraform and Ansible configurations according to your infrastructure and deployment requirements.
- Ensure proper AWS credentials are configured for Terraform to provision resources.
- Review and modify the Docker Compose file and Dockerfiles as needed for your specific application requirements.
