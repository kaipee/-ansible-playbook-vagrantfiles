# Ansible Playbook Vagrantfiles

This is a collection of Vagrantfile templates for testing Ansible Playbooks in an isolated environment.

## Requirements

Ensure the Vagrant Provider for your chosen Vagrantfile is installed as per the [official instructions for installing Providers](https://www.vagrantup.com/docs/providers).

## Instructions

Save one of the files, depending on desired Vagrant Provider, in the root directory of your Ansible Playbook and rename it to `vagrantfile`.

The Vagrantfile template will deploy a local virtual environment and automatically provision it using your Ansible Playbook.

If your Playbook file isn't named **playbook.yml**, you will need to replace `playbook.yml` in the Vagrantfile with the name of your playbook.

### Exclude .vagrant working directory

In order to ensure the Vagrant virtual environment (Box) doesn't get committed to version control alongside your Playbook, create a **.gitignore** file with the following contents:

```config
.vagrant/
```

## Usage

**Provision an environment**

```sh
vagrant up
```

**Login to the environment**

```sh
vagrant ssh
```

**Destroy an environment**

```sh
vagrant destroy
```
