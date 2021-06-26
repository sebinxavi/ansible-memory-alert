# Ansible Playbook for High Memory Notification alerts

This Ansible Playbook will helps you to Monitor and enable notifications for High Memory alert via Email.

## Prerequisites
- Ansible version - 2.9
- Linux Master Server 
- Client Servers - CentOS
- SSH PEM key for Remote Servers
- SSH User with sudo privilege

### Usage

This script will perform following operations;

- Update all Packages in client servers
- Instal systat and bc package
- Copy Get-Memory-Utilization.sh script to client servers
- Apply the logic using ansible "WHEN" condition and print message accordingly
- Send Email when MEMORY utilization become abnormal (Greater than 90%)

# Ansible Installation

```sh
$ yum -y install ansible
```

## How to configure

With Ansible installed, you are ready to setup the email notification by following the below steps.

```sh
$ git clone https://github.com/sebinxavi/ansible-memory-alert.git
$ cd ansible-memory-alert
```

##### Open the file 'hosts' and edit the Remote hosts details.
The Sample format is provided below,
```sh
[centos]
172.31.47.208  ansible_user=centos ansible_port=22 ansible_ssh_private_key_file=centos.pem
```

- Add a Group name for the remote hosts. Example: centos/ubuntu
- Add the Remote Host IP addresse. Example: 172.31.43.55
- Add the Remote SSH User. Example: centos
- Add the SSH port number: Example: 22
- Import the SSH key file to the same location in which we are going to run the Ansible command and add the key name to the file hosts

#### Open the ansible playbook file "memory.yml" and edit the email details.

```sh
host: smtp.gmail.com
port: 587
username: "test1@gmail.com"
password: "password"
to: John Sam <johnsam@gmail.com>
```
- host : Hostname of Email Server
- port: SMTP port number
- username: Username of email
- password: Gmail app password or your email normal password
- to: Recpient Email address

Run the ansible-playbook from the master server by below command,

```sh
$ ansible-playbook -i hosts memory.yml
```

## Results:
You will receive an Ansible Email notification if MEMORY usage exceeds more than 90%.

## Author
Created by [@sebinxavi](https://www.linkedin.com/in/sebinxavi/) - feel free to contact me and advise as necessary!

<a href="mailto:sebin.xavi1@gmail.com"><img src="https://img.shields.io/badge/-sebin.xavi1@gmail.com-D14836?style=flat&logo=Gmail&logoColor=white"/></a>
<a href="https://www.linkedin.com/in/sebinxavi"><img src="https://img.shields.io/badge/-Linkedin-blue"/></a>
