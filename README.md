## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Picture](Diagram/Azure_Virtual_Network.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the `install-elk.yml` file may be used to install only certain pieces of it, such as Filebeat.

  - _![Filebeat Playbook](Ansible/filebeat-playbook.yml)._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build
  


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting outsiders to SSH into the network.
- _What aspect of security do load balancers protect? What is the advantage of a jump box?_
  - The aspect of security that load balancers provide are redundancy and mitigation from DDoS attacks. The advantages of the jumpbox is to reduce the attack vector surface so that only one machine is allowed to SSH into the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configurations and system logs.
- _What does Filebeat watch for?_
  - Filebeat watches for SSH logins, sudo commands, and syslogs  
- _What does Metricbeat record?_
  - Metricbeat watches for CPU, memory, and network consumption usage. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    |          |            |                  |
| TODO     |          |            |                  |
| TODO     |          |            |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the `Jumpbox` machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Web-1: Ip
- Web-2: 
- Web-3: 10.0...
- Elk-VM: 10.1...

Machines within the network can only be accessed by `Jumpbox w/ Ansible Container`.
- _Which machine did you allow to access your ELK VM? What was its IP address?_
  - The `Jumpbox` with IP Address: 10.0.. 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes, only from my personal machine              | 10.0.0.1 10.0.0.2    |
| Web-1          | HTTP - Yes ---- SSH - No                     |                      |
| Web-2          | HTTP - Yes ---- SSH - No                       |                      |
| Web-3          | HTTP - Yes ---- SSH - No                       |                      |
| Elk-VM      | HTTP - Yes ---- SSH - No                       |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _What is the main advantage of automating configuration with Ansible?_
  - It allows us to save time and human error when configuring multiple machines.

The playbook implements the following tasks:
- _In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
  - We installed docker
  - We installed python to support the container
  - We increased the memory to support the minimum RAM requirements of 4GB
  - We installed the ELK container and opened up certain ports
  - We started the container to allow ELK to run

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Elk-Container](Diagram/ELK_container.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _List the IP addresses of the machines you are monitoring_
   - Public IP of Web-1 : 52.149.41.110 
Private Ip of Web-1: 10.0.0.5  
    - Public IP of Web-2: 52.149.41.110
Private IP of Web-2: 10.0.0.6
    - Public Ip of Web-3: 
Private IP of Web-3: 10.0.0.8

We have installed the following Beats on these machines:
- _Specify which Beats you successfully installed_
  - We installed `filebeat` and `metricbeat`.  

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
  - Filebeat:
  - Metricbeat:

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the `/etc/ansible/files/filebeat-config.yml` file to `/etc/filebeat/filebeat.yml`.
- Update the `/etc/filebeat/filebeat.yml` file to include the ip of kibana.
  ```
  output.elasticsearch:
  hosts: localhost:9600
  username: "elastic"
  password: "<password>"
  setup.kibana:
  host: localhost:5601
  ```
- Run the playbook, and navigate to `ELK-VM` to check that the installation worked as expected.

_Answer the following questions to fill in the blanks:_
- _Which file is the playbook?_
  - The file that is the playbook is the `install-elk.yml` file
 - _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
    - You can edit the `/etc/ansible/hosts` file to specify which group of machiens you would like to install the elk server on. In this case, the `Elk-VM` was located in the `elk` group of the hosts files, therefore the playbook will only configure the servers under that group.   
- _Which URL do you navigate to in order to check that the ELK server is running?_
  - http://52.179.213.172:5601/
 
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
