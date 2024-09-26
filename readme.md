# GitLab Runner and Docker Installation Playbook

This playbook installs Docker and GitLab Runner on your servers.

## Requirements

- Ansible >= 2.9
- Molecule >= 3.0
- Vagrant >= 2.2
- VirtualBox >= 6.1

## Production Inventory

The production inventory file should contain information about the hosts where Docker and GitLab Runner will be installed. You need to update the `production` inventory file with your server details.

Example of the `production` file:

```ini
[gitlab_runner_docker]
production ansible_ssh_host=192.168.50.1 ansible_ssh_port=2211 ansible_ssh_user=vagrant ansible_python_interpreter=/usr/bin/python3
```

Modify the following parameters:

- `ansible_ssh_host`: Set this to the IP address of your server.
- `ansible_ssh_port`: SSH port of your server.
- `ansible_ssh_user`: SSH user for your server.
- `ansible_python_interpreter`: Path to Python interpreter on your server.

## Running the Playbook

To run the playbook on your server and install Docker and GitLab Runner, use the following command:

```bash
ansible-playbook -i inventory/production playbook.yml
```

This will install Docker and GitLab Runner on the servers defined in the production inventory.

## Molecule Testing

This project uses Molecule to test the playbook with Vagrant and VirtualBox. Molecule is a testing tool that creates virtual machines to simulate server environments and run Ansible playbooks.

### Installing the Molecule Vagrant Plugin

Before running Molecule tests, make sure to install the necessary plugins, including the Molecule Vagrant plugin:

```bash
pip install molecule molecule-vagrant
```

### Running Molecule Tests

To run Molecule tests locally:

1. Ensure that Vagrant and VirtualBox are installed.
2. Run the following command to execute Molecule tests:
   ```bash
   molecule test
   ```

This will spin up virtual machines, run the playbook, and verify the results.

### Requirements for Molecule Tests

- Install Vagrant and VirtualBox before running the tests:
  - [Vagrant](https://www.vagrantup.com/downloads)
  - [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

### Molecule Vagrant Configuration

Molecule uses Vagrant as the provider to run the tests on virtual machines. The configuration for Vagrant is in the `molecule/default/molecule.yml` file.

Example configuration:

```yaml
driver:
  name: vagrant

platforms:
  - name: ubuntu20
    box: bento/ubuntu-20.04
    memory: 2048
    cpus: 2
  - name: ubuntu22
    box: bento/ubuntu-22.04
    memory: 2048
    cpus: 2
```

This configuration runs the playbook on Ubuntu 20.04 and 22.04.

## Conclusion

Follow the steps above to configure the inventory, run the playbook, and test it using Molecule with Vagrant. If you encounter any issues, ensure that all the necessary dependencies and plugins are installed and the configurations are correct.