# Automated-ELK-Stack-Deployment
Diagramming and Documentation of ELK Stack Project 


The files in this repository were used to configure the network depicted below.

![Network Diagram](/Diagrams/Project-Netwotk-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

- elk-playbook.yml
- filebeat-playbook.yml
- metricbeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly effective, in addition to restricting access to the network.

* What aspect of security do load balancers protect?
 - They prevent unwanted or unauthorized traffic from reaching the     
  application.
 - The off-loading function of loadbalancer defends an organization  
  against DDoS attacks.

What is the advantage of a jump box?
 They add a security layer to the web servers them from being exposed to 
 the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configuration files and system files.

What does Filebeat watch for?
 They watch for log files or log events.

What does Metricbeat record?
 They record Metrics from ongoing services on the server such as CPU.







The configuration details of each machine may be found below.
 
| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump-Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Server   | 10.0.0.5   | Linux            |
| Web-2    | Server   | 10.0.0.6   | Linux            |
| ELK-VM   | Server   | 10.1.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 14.200.10.147(Local Host Public IP Address)

Machines within the network can only be accessed by Jump-Box.
- Which machine did you allow to access your ELK VM? 
  My personal computer 
- What was its IP address?
 Public IP Address 14.200.10.147

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses   |
|----------|---------------------|----------------------  |
| Jump-Box | Yes                 |10.0.0.5 10.0.0.6       |
| Web-1    | No                  |52.168.165.249          |
| Web-2    | No                  |52.168.165.249          |
| ELK-VM   | Yes                 |52.233.88.37            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. 
No configuration was performed manually, which is advantageous because it is flexible and allows changes to be made within any of the VMs associated with it.

The playbook implements the following tasks:

1. Install Docker.io
2. Install python3-pip
3. Install Docker Python Module
4. Increase Virtual Memory
5. Download and launch a Docker ELK Container 


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


![Docker PS](/Images/ELK-VM-Docker-PS.png)




### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- Web-1     10.0.0.5
- Web-2     10.0.0.6
- ELK-VM    10.1.0.6

We have installed the following Beats on these machines:
- Filebeat and Metricbeat installed on Web-1 and Web-2

These Beats allow us to collect the following information from each machine:
- Filebeat monitors log files and log events.

- Metricbeat looks out for any information in the file system which has been manipulated.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

**Filebeat**
- Copy the filebeat-configuration.yml file to /etc/ansible/roles/files.
- Update the filebeat-configuration.yml file to include the ELK private IP in lines 1106 and 1806.
- Run the playbook, and navigate to http://52.233.88.37:5601 (ELK-VM public IP) to check that the installation worked as expected.

![Filebeat Status](/Images/Filebeat-Module-Status.png)

**Metricbeat**
- Copy the metricbeat-configuration.yml file to /etc/ansible/roles/files.
- Update the metricbeat-configuration.yml file to include the ELK private IP in lines 62   and 95.
- Run the playbook, and navigate to http://52.233.88.37:5601 (ELK-VM public IP) to check that the installation worked as expected.

![Metricbeat Status](/Images/Metricbeat-Module-Status.png)

Answer the following questions to fill in the blanks:
-  Which file is the playbook? ELK-playbook.yml
-  Where do you copy it? /etc/ansible
-  Which file do you update to make Ansible run the playbook on a specific machine?  Hosts file 
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?By using the IPs of the respective servers.
- Which URL do you navigate to in order to check that the ELK server is running?
http://[ELK-VM-ip]:5601/app/kibana     


![Kibana](/Images/Kibana-Homepage.png)

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.


-	Filebeat playbook
-  To create the filebeat-configuration.yml file: nano filebeat-configuration.yml. For this, I used the filebeat configuration file template.

-  To create the playbook: nano filebeat-playbook.yml



![filebeat](/Images/filebeat-playbook.png)


-	To run the playbook: ansible-playbook filebeat-playbook.yml




-	Metricbeat playbook

-  To create the metricbeat-configuration.yml file: nano metricbeat-configuration.yml. For this, I used the metricbeat configuration file template.

-  To create the playbook: nano metricbeat-playbook.yml

---![metricbeat](/Images/metricbeat-playbook.png)

-	To run the playbook: ansible-playbook metricbeat-playbook.yml
