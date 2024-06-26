# Ansible Role: ec2_create

An Ansible role to create Ubuntu and Amazon Linux EC2 instances on AWS.

## Requirements

- Ansible 2.9 or higher
- AWS credentials with permissions to create EC2 instances

## Prerequisites

Before running the playbook, make sure you have the following prerequisites set up:

1. Generate a vault password file using OpenSSL:

```bash
openssl rand -base64 32 > vault.pass
```

2. Create a vault file (pass.yml) using Ansible Vault with the generated password file:

```bash
ansible-vault create pass.yml --vault-password-file vault.pass
```

3. Store your AWS credentials (access key and secret key) in the created vault file (pass.yml). The file should look like this:

```yaml
access_key: YOUR_AWS_ACCESS_KEY_ID
secret_key: YOUR_AWS_SECRET_ACCESS_KEY
```

## Role Variables

The following variables can be customized:

- `access_key`: AWS access key ID.
- `secret_key`: AWS secret access key.
- `region`: AWS region where EC2 instances will be created.
- `instance_type`: EC2 instance type (e.g., t2.micro).
- `key_pair`: Name of the SSH key pair to use for instance access.
- `security_group`: ID of the security group for EC2 instances.
- `availability_zone`: Name of tha availability zone in which the EC2 instances will be created.
- `assign_public_ip`: Whether to assign a public IP address to instances (true or false).
- `env`: Environment tag for the instances.
- `ec2_instances`: List of dictionaries specifying the EC2 instances to create, including image IDs and instance names.

## Dependencies

No dependencies on other roles.

## Example Playbook

```yaml
- name: EC2 Instances Creation Playbook
  hosts: localhost
  connection: local
  vars_files:
    - "<your_vault_file_location>"   # This file (pass.yml) provides encrypted variables for the ec2_create role
  roles:
    - ec2_create
```

## Running the Playbook

To run the playbook, use the following command:

```bash
ansible-playbook <your_playbook_name> --vault-password-file <your_vault_password_file_location>
```

## License

MIT

## Author Information

Author: Surya