# Elk-Stack-Project
Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
Note: The following image link needs to be updated. Replace diagram_filename.png with the name of your diagram image file.

https://drive.google.com/file/d/118IHLqR0Wmz6CUkc6ycnpx_VHZmnpWNU/view?usp=sharing
[Dominik Holt - Homework File_ Cloud Security.drawio.pdf](https://github.com/DomH29/Elk-Stack-Project/files/9264700/Dominik.Holt.-.Homework.File_.Cloud.Security.drawio.pdf)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

# my-playbook.yml
---
- name: Config Web VM with Docker
  hosts: webservers
  become: true
  tasks:
  - name: Install docker.io
    apt:
      name: docker.io
      state: present
      update_cache: yes
  - name: Install pip3
    apt:
      name: python3-pip
      state: present
      force_apt_get: yes
  - name: Install docker via pip
    pip:
      name: docker
      state: present
  - name: Download a docker web container
    docker_container:
      name: dvwa
      image: cyberxsecurity/dvwa
      state: started
      published_ports: 80:80
      restart_policy: always
  - name: Enable docker service
    systemd:
      name: docker
      enabled: yes
Footer
This document contains the following details:

Description of the Topologu
Access Policies
ELK Configuration

Beats in Use
Machines Being Monitored


How to Use the Ansible Build


Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly reliable, in addition to restricting access to the network.

What aspect of security do load balancers protect? What is the advantage of a jump box? Helps to mitigate DDos attacks

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network traffic and system files.

What does Filebeat watch for? It helps us to maintain and monitor the network through single VM gateway

What does Metricbeat record? Gives us a sense of how well a network is opperating

The configuration details of each machine may be found below.

Note: Use the Markdown Table Generator to add/remove values from the table.



Name
Function
IP Address
Operating System




Jump Box
Gateway
10.0.0.1
Linux

Name	Function	IP Address	Operating System
Jump Box	Gateway	10.0.0.7	Linux ubuntu 18.04
Web-1	Web server	10.0.0.5	Linux ubuntu 18.04
Web-2	Web server	10.0.0.6	Linux ubuntu 18.04
Web-3	Web server	10.0.0.9	Linux ubuntu 18.04
Elk server	Monitoring	10.1.0.4	Linux ubuntu 18.04



Access Policies
The machines on the internal network are not exposed to the public Internet.
Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

Add whitelisted IP addresses: 76.209.224.121

Machines within the network can only be accessed by the JumpBox.

Which machine did you allow to access your ELK VM? What was its IP address? the JumpBoxProvisioner, 10.0.0.7
A summary of the access policies in place can be found in the table below.



| Name               | Publicly Accessible | Allowed IP Addresses |
|--------------------|---------------------|----------------------|
| JumpBoxProvisioner | Yes (SSH p22)       | 20.84.53.206         |
| ELK-VM             | Yes (RDP p3389)     | 20.84.53.206         |
| Web-1              | Yes (HTTP p80)      | 20.84.53.206         |
| Web-2              | Yes (HTTP p80)      | 20.84.53.206         |
| Web-3              | Yes (HTTP p80)      | 20.84.53.206         |
| Elk server         | Yes (HTTP p5601)    | 20.84.53.206         |
| Elk Server         | Yes (SSH p22)       | 20.84.53.206         |














Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because..

Target Machines & Beats
This ELK server is configured to monitor the following machines: 

JumpBoxProvisioner: 10.0.0.7
Web-1: 10.0.0.8
Web-2: 10.0.0.9


We have installed the following Beats on these machines:

TODO: Specify which Beats you successfully installed 

Filebeat
Matricbeat

These Beats allow us to collect the following information from each machine:

Filebeat monitors log files or events and forwards them to ElasticSearch
Metricbeat collects metrics from the server or operarting system

Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:

Copy the configuration file to Ansible container.
Update the configuration file to include the ELK server's IP address
Run the playbook, and navigate to Kibana to check that the installation worked as expected.

TODO: Answer the following questions to fill in the blanks:

Which file is the playbook? Where do you copy it? filebeat-playbook.yml and metricbeat-playbook.yml, etc/ansible/files/
Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? filebeat-config.yml, metricbeat-config.yml

_Which URL do you navigate to in order to check that the ELK server is running? 

