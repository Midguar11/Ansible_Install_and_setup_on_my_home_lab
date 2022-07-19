# Install and Setup Ansible my home lab server ( going to use MiniConda )

- Home lab: Dell R720 ( ESXi )
- Create VM in home lab, with ubuntu template
- Login

      ssh-keygen -t rsa -b 4096
      /home/user/.ssh/Ansible
      ls -l ~/.ssh

- when add server ssh key :

      ssh-copy-id -i ~/.ssh/Ansible  user@ip

- when cheking this working

      ssh -i ~/.ssh/Ansible  root@ip apt update

- Insall miniconda  " virtual directory " emulate hardware and tools free environment. All in the pack.

      curl -OL https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
      ls
      bash Miniconda3-latest-Linux-x86_64.sh

- setup, and accept license, pgdown , yes, enter, yes
      
      exec bash -l
      conda create -n ansible-dev python=3 
      ls miniconda3/envs

- add ansible-dev to sudoer
      
      visudo

- user sudoer specification new user" midguard ALL=(ALL) NOPASSWD:ALL "
 - user sudoer specification new user" ansible-dev ALL=(ALL) NOPASSWD:ALL

- change user ansible dev: 

      conda activate ansible-dev
      python --version

- paste this > deb http://ppa.launchpad.net/ansible/ansible/ubuntu/ trusty main

      sudo apt install gnupg
      sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 93C4A3FD7BB9C367
      sudo apt update 
      sudo apt install ansible
      ansible-playbook --version
      sudo mkdir /etc/ansible
      sudo nano /etc/ansible/hosts

- " [nginx]
10.10.10.10
[jenkins]
10.10.0.13"

- Save and next step test

      ansible all -u midguard -m ping --private-key ~/.ssh/Ansible

# If EC2 ( AWS Instances):

- Connect Ansible Controller
- cat Ansible.pub
- Go AWS Add new keypair paste ansible.pub
- Use this keypair new instances
- completed instaces, connect to

      ssh -i ~/.ssh/Ansible ec2-user@54.172.185.67
      sudo su -
      sudo adduser midguard
      sudo nano /etc/sudoers

- add last line " midguard ALL=(ALL) NOPASSWD:ALL  "

      sudo su - midguard
      mkdir .ssh
      chmod 700 .ssh
      cd .ssh
      touch authorized_keys
      nano authorized_keys

- copy here from Asnible.pub content
- save
- exit
- exit
- ssh -i ~/.ssh/Ansible midguard@54.172.185.67

# What we control must be set on all servers:

      sudo -i
      nano /etc/sudoers.d/username
      username ALL=(ALL) NOPASSWD:ALL
      
  - save and exit root try back root sudo -i, If it doesn't ask for a password. Everything is alright


# Install plugin

      ansible-galaxy collection install amazon.aws

# Install on Hosts

sudo apt-get install python

# Setup Controled Client

- connect to Asnible controll

            git clone git@github.com:Midguar11/Labor_auto_updater.git

