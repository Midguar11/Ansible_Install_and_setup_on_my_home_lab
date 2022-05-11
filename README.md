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

      ssh -i ~/.ssh/ansible  root@ip apt update

- Insall miniconda  " virtual directory " emulate hardware and tools free environment. All in the pack.

      curl -OL https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
      ls
      bash Miniconda3-latest-Linux-x86_64.sh

- setup, and accept license, pgdown , yes, enter, yes
      
      exec bash -l
      conda create -n ansible-dev python=3 
      ls miniconda3/envs
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

      ansible all -u user -m ping --private-key ~/.ssh/Ansible