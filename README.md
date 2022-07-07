# Ansible Playbook Vagrantfiles

This is a collection of Vagrantfile templates for testing Ansible Playbooks in an isolated environment.

## Requirements

Ensure the Vagrant Provider for your chosen Vagrantfile is installed as per the [official instructions for installing Providers](https://www.vagrantup.com/docs/providers).

## Instructions

### Vagrantfile usage

Save one of the files, depending on desired Vagrant Provider, in the root directory of your Ansible Playbook and rename it to `vagrantfile`.

The Vagrantfile template will deploy a local virtual environment and automatically provision it using your Ansible Playbook.

If your Playbook file isn't named **playbook.yml**, you will need to replace `playbook.yml` in the Vagrantfile with the name of your playbook.

### Configure the virtual environment

Configure the testing environment depending on your needs using the variables contained at the start of each Vagrantfile.

#### Example

```ruby
BOX_DISTRO = "ubuntu"
BOX_RELEASE = "bionic64"
BOX_VERSION = ">=v20220705.0.0"
BOX_URL = "https://app.vagrantup.com/ubuntu/boxes/bionic64"

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

### Provision an environment

```sh
vagrant up
```

Once the environment is up and running it can be accessed at **127.0.0.1**. For security the environment is configured to only listen on this interface.

### Login to the environment

```sh
vagrant ssh
```

### Destroy an environment

```sh
vagrant destroy
```
