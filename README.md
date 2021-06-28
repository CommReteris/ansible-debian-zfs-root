# Debian ZFS on root bootstrap

This project is a set of ansible playbooks to automate the installation of a
Debian system with an un-encrypted ZFS on root system. (encryption is todo)


## Assumptions on the setup

- ⚠️ The disk(s) can be erased. ⚠️
- The system supports UEFI.
- You want Debian Buster
- You have ansible >2.10 installed on your system.
- You have a wired connection on your machine.


## Installation

### Preparing the system

The first step is to setup a live environment in which we will be able to start
the installation.

You will need to start by getting a
[Debian live CD](https://cdimage.debian.org/cdimage/weekly-live-builds/amd64/iso-hybrid/)
and boot your system with it.

You will then need to install an ssh server an set it up:

```
sudo apt update
sudo apt install openssh-server
sudo systemctl start sshd
```

And gather the connection information:

```
ip addr show scope global | grep inet
```

### Preparing the inventory

⚠️⚠️⚠️

This is the most critical part of the setup and later steps _**will wipe**_ disks. Be careful with what you set here. You have been warned.

⚠️⚠️⚠️


Edit the inventory file [./inventory.yml](./inventory.yml) and fill in the fields according to the inline documentation.


### Starting the installation

⚠️⚠️⚠️ This will wipe the disks you have selected and you will **loose all data** on them. You have been warned.

In order to install the system, run:

```
ansible-playbook --diff playbook.yml
```
