## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Description of Topology

[Diagram](Images/Network_Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. 

  ![Install Docker Python](Playbook/Install_Docker_Python_FirstPlaybook.yml)
  ![Install Elk](Playbook/Elk_Install.yml)
  ![Install Elk PIP APT](Playbook/Elk_pip_apt_ansible.yml)
  ![Install Filebeat-playbook](filebeat-playbook.yml)
  ![Install metric-playbook](metricbeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- What aspect of security do load balancers protect? Load Balancer protect from DDos Attacksy shiftting attack traffic 
  What is the advantage of a jump box? Benefits of Jumpbox is single node that needs to be secured and monitored, also you create playbook on one server and deploy to hundred servers

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- What does Filebeat watch for? Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- What does Metricbeat record? Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump-Box | Gateway  | 10.1.0.4   | Linux            |
| Web-1    |DVWAServer| 10.1.0.6   | Linux            |
| Web-2    |DVWAServer| 10.1.0.7   | Linux            |
Elk-Server-1|ELKServer| 10.0.0.5   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. 
Access to this machine is only allowed from the following IP addresses: 1.145.197.166

Machines within the network can only be accessed by Jump-Box-Provisioner.
Which machine did you allow to access your ELK VM? Jump-Box-Provisioner , 1.145.197.166
 What was its IP address? 10.1.0.4 , 10.1.0.6, 10.1.0.7

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 1.145.197.166        |
| Web-1    | No                  | 10.1.0.4             |
| Web-2    | No                  | 10.1.0.4             |
Elk-Server-1| yes                | 1.145.197.166, 10.1.0.4 |

[Acces Policy](Images/AccesPoliciesforRTX_RED_SG.PNG)
[Access Policy for Elk Server](AccessPoliciesforELK_Server.PNG)


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because since you have multiple installation , commands etc using one playbook and do not need to create multiple
- What is the main advantage of automating configuration with Ansible? Single Playbok to do many things in one go and also can be deployed on multiple servers with consistency

The playbook implements the following tasks:	
Install: docker.io
Install: python-pip
Install: docker
Command: sysctl -w vm.max_map_count=262144
Also Publish Ports
Launch docker container: elk

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Docker PS](Docker_PS.PNG)



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring
Web1 : 10.1.0.6 
Web 2: 10.1.0.7


We have installed the following Beats on these machines:
Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:

File Beat Collects the changes done

Metric Beat Collects statisticsand metric 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible/files.
- Update the /etc/ansible/hosts file to include Elk Server(10.0.0.5) and Web Server(10.1.0.6, 10.1.0.7)
- Run the playbook, and navigate to http://40.122.114.123:5601/ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running? http://40.122.114.123:5601/

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._


nano filebeat-playbook.yml
nano metricbeat-playbook.yml
ansible-playbook filebeat-playbook.yml
ansible-playbook metricbeat-playbook.yml
ansible webservers -m command -a "sudo docker ps -a"
ansible ELK -m command -a "sudo docker ps -a"