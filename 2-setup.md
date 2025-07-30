# Setup

Setup of Ansible on Ubuntu24

```

## Update OS Packages
sudo apt update && sudo apt upgrade -y

## Install Required Dependencies
sudo apt install -y software-properties-common

## Add Ansible Official PPA (from Ansible team)
sudo add-apt-repository --yes --update ppa:ansible/ansible

## Install Ansible
sudo apt install -y ansible

##Verification of Installation
ansible --version

```

Setup of Ansible on Redhat9

First we need to attach the subscription from redhat using `subscription-manager register` and then attach the subscription using `subscription-manager attach --auto`.
If we have satellite server present then use that as well.

```

## Enable Required Repositories
sudo subscription-manager repos \
--enable ansible-2.9-for-rhel-9-$(arch)-rpms \
--enable codeready-builder-for-rhel-9-$(arch)-rpms

## Install Ansible
sudo dnf install -y ansible

## Verify Install
ansible --version

```