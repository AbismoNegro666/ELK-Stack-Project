## ELK stack project

Elk stack project; week13

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

- [ELK Environment](Diagram/ELK-NetworkDia.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat and Metricbeat

- [ELK deployment](Ansible/elk-pb.yml)
- [filebeat playbook](Ansible/filebeat-pb.yml)
- [filebeat-config.yml](Ansible/filebeat-config.yml)
- [metricbeat playbook](Ansible/metricbeat-pb.yml)
- [metricbeat-config.yml](Ansible/metricbeat-config.yml)

This document contains the following details:

- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly effecient and secure by spreading workloads across multiple servers to prevent overloading servers. This feature will optimize productivity, and maximize uptime in addition to restricting unauthorized access to our network. Load balancers eliminate single-points of failure in the event one server is decommissioned due to ovewhelming traffic. On top of the load balancer providing security, we have our entire network in a security zone. We setup this network so that our VM's are only accessed via a jump box.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the machine metrics or quantifiable data (metricbeat) and system files (filebeat).

- Filebeat's function is to monitors/imports log file data to the ELK stack for analysis via LogStash > ElasticSearch > and finally visualized on Kibana.

- Metricbeat ships quantifiable data to the ELK stack such as CPU usage. Metric will allow users to diagnose machine resource issues.

The configuration details of each machine may be found below.


|    Name    |  Function  |   IP Address   |   OS  |
|:----------:|:----------:|:--------------:|:-----:|
|   JumpBox  |   Gateway  | 20.213.125.144 | Linux |
|    Web-1   |    DVWA    |    10.0.0.4    | Linux |
|    Web-2   |    DVWA    |    10.0.0.5    | Linux |
| Project-VM | ELK server |    10.1.0.4    | Linux |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 76.87.86.157 (which is the local host)

Machines within the network can only be accessed by Jump box via docker.

Which machine did you allow to access your ELK VM?
- The jump box machine

What was its IP address?_
- 20.213.125.144

A summary of the access policies in place can be found in the table below.

|    Name    | Publicly Accessible | Allowed IP Address |
|:----------:|:-------------------:|:------------------:|
|   JumpBox  |         Yes         |    76.87.86.157    |
|    Web-1   |          No         |   20.213.125.144   |
|    Web-2   |          No         |   20.213.125.144   |
| Project-VM |          No         |   20.213.125.144   |


### Elk Configuration

Ansible was used to automate configurations of the ELK machine. No configuration was performed manually, which is advantageous because it allows for continuity across all machines and keeps configurations the same which inturn minimizes user-errors. 

The playbook implements the following tasks:

In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.
- Open terminal on local machine and ssh into JumpBox 'ssh sysadmin@20.213.125.144'
- Once in the JumpBox machine; start>attach to docker container 'sudo docker start keen_uler' > 'sudo docker attach keen_euler'
- Create a ansible playbook on YAML file with instruction on how to download and install ELK server [ELK playbook](Ansible/elk-pb.yml)
- Once completed and all files configured we can run the ansible playbook
- Running playbook via ansible ansible-playbook elk-pb.yml
- Once ran successfully, ssh into ELK-server machine 'ssh sysadmin@10.1.0.4' to confirm proper installation.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Container listing in the ELK server AKA 'Project-VM'](Diagram/Project-VM ELK docker Container.jpg)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

List the IP addresses of the machines you are monitoring
	Web-1: 10.0.0.4
	Web-2: 10.0.0.5

We have installed the following Beats on these machines:

- Filebeats has been installed on machines 10.0.0.4 (w1) and 10.0.0.5(w2) <insert module status img>
- Metricbeatshas been installed on machines 10.0.0.4 (w1) and 10.0.0.5(w2) <insert module status img>

These Beats allow us to collect the following information from each machine:

- Filebeat: A log file is a data file that contains information about usage activities, and operations within an machine. Web browser log files could be used for security analysis, such as review user sessions.

- Metricbeat: A metric file is data file that contains informatino about speficic system quantifiable measures. A CPU log could show its usage at specific interval during its usage, which could be used for diagnostic date, given there was an issue. 

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the <filebeat-config.yml file along with path> file to /etc/ansible/.
- Update the the <filebeat-config.yml> to file to reflect your ELK-server's private IP address on lines #1106 and #1806.
- Run the playbook, ensure results are error-free and navigate to http://<localhost>:5601 on your machines browser to check that the installation worked as expected.

Answer the following questions to fill in the blanks:

- Which file is the playbook? 
	- filebeat playbook: [filebeat playbook](Ansible/filebeat-pb.yml)
	- metricbeat playbook: [metricbeat playbook](Ansible/metricbeat-pb.yml)
- Where do you copy it? 
	'/etc/ansible/files'
- Which file do you update to make Ansible run the playbook on a specific machine?
	'/etc/ansible/hosts'
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?
	Navigate to YAML file '/etc/ansible/hosts' add you machines' private IP address to the 	appropriate host which could be 'webserver' and 'elk' (which was 	 manually named). Webserver host is designated for machine's 'web-1' and 'web-2' and elk host is for the 'ProjectVM' or ELK server machine.
- Which URL do you navigate to in order to check that the ELK server is running?
	curl http://localhost:5601
