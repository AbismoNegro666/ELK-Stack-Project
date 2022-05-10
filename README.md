# Elk_Stack
Elk stack project; week13
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[ELK Environment](Diagram/ELK-NetworkDia.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - [ELK environment deployment playbook](Ansible/elk-pb.yml)

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

- Filebeat's function is to import or 'ships' log file data to the ELK stack for analysis.
- Metricbeat ships quantifiable data to the ELK stack such as CPU usage. Metric will allow users to diagnose machine resource issues.

The configuration details of each machine may be found below.

| Name       | Function | IP Address | OS    |
|------------|----------|------------|-------|
| Jump Box   | Gateway  | 10.0.0.x   | Linux |
| Web-1      |  DVWA    | 10.0.0.x   | Linux |
| Web-2      |  DVWA    | 10.0.0.x   | Linux |
| ELK Server |   ELK    | 10.1.0.x   | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 76.87.86.xxx

Machines within the network can only be accessed by Jump box via docker.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
- The jump box machine (20 is the only machine is able to access the ELK server via Docker container.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
|  Jump Box  |         YES         |     76.87.86.XXX     |
|    Web-1   |          NO         |     20.213.125.144   |
|    Web-2   |          NO         |     20.213.125.144   |
| ELK Server |          NO         |     20.213.125.144   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which allows for continuity across all machines.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- Filebeats has been installed on machines 10.0.0.4 (w1) and 10.0.0.5(w2)
- Metricbeatshas been installed on machines 10.0.0.4 (w1) and 10.0.0.5(w2)

These Beats allow us to collect the following information from each machine:
- Filebeat:
- Metricbeat:
- WinLogBeat:

- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
