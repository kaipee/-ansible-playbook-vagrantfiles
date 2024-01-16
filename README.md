# Ansible Playbook Vagrantfiles

This is a collection of Vagrantfile templates for testing Ansible Playbooks in an isolated environment.

## Requirements

Ensure the Vagrant Provider for your chosen Vagrantfile is installed as per the [official instructions for installing Providers](https://www.vagrantup.com/docs/providers).

## Instructions

### Vagrantfile usage

Save one of the files, depending on desired Vagrant Provider, in the root directory of your Ansible Playbook and rename it to `vagrantfile`.

The Vagrantfile template will deploy a local virtual environment and automatically provision it using your Ansible Playbook.

If your Playbook file isn't named **playbook.yml**, you will need to replace `playbook.yml` in the Vagrantfile with the name of your playbook.

The Vagrantfile will make use of Ansible Roles. Make sure to install the Ansible Roles before starting with vagrant:

```sh
ansible-galaxy role install --force -r roles/requirements.yml
```

### Configure the virtual environment

Configure the testing environment depending on your needs using the variables contained at the start of each Vagrantfile.

Boxes and their details can be found at https://app.vagrantup.com/boxes/search .

VM configurations should be changed to meet your needs.

Variables `BOX_VERSION` and `BOX_URL` are **optional**.

#### Example

```ruby
BOX_DISTRO = "ubuntu"
BOX_RELEASE = "bionic64"
BOX_VERSION = ">=v20220705.0.0"  # optional
BOX_URL = "https://app.vagrantup.com/ubuntu/boxes/bionic64"  # optional

VM_NAME = "ubuntu-playbook"
VM_MEMORY = 2049
VM_CPU = 2
VM_PORT_GUEST = 80
VM_PORT_HOST = 8080
VM_DISPLAY_GUI = false
```

### Exclude .vagrant working directory

In order to ensure the Vagrant virtual environment (Box) doesn't get committed to version control alongside your Playbook, create a **.gitignore** file with the following contents:

```config
.vagrant/
```

## Usage

### Install any Ansible Roles

```sh
ansible-galaxy role install --force -r roles/requirements.yml
```

### Provision an environment

```sh
vagrant up
```

Once the environment is up and running it can be accessed at **127.0.0.1**. For security the environment is configured to only listen on this interface.

### Re-provision the environment

If the environment is up and running but there are issues with the Playbook, after editing the Playbook you can simply re-provision it without re-deploying the environment.

```sh
vagrant provision
```

### Login to the environment

```sh
vagrant ssh
```

The environment can be accessed via SSH in order to troubleshoot Playbook provisioning issues.

The Ansible Playbook will be mounted in the environment under `/vagrant/` .

### Destroy an environment

```sh
vagrant destroy -f
```
