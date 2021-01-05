## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


![ ](/Images/elk_project_network_diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible and playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  - [Filebeat-playbook.yml](https://github.com/kwekumills/Kweku_Projectassignment/blob/main/Ansible/filebeat-playbook.yml)

  - [elk-playbook.yml](https://github.com/kwekumills/Kweku_Projectassignment/blob/main/Ansible/elk-playbook.yml)

  - [playbook.yml](https://github.com/kwekumills/Kweku_Projectassignment/blob/main/Ansible/playbook1.yml)






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
- What aspect of security do load balancers protect? What is the advantage of a jump box?

Load balancers protect servers from attacks such as denial of service which affects availability of servers, they also offer a health probe function to control traffic sent to various machines or servers. 
The Jump box servers as an administrative server to administrate other servers in the resource group, the jumpbox provides extra hardened security. In this scenario, the only way to get access to the web servers in the red team resource group is through the Jumpbox which isn't easily accessible even with when attackers try to brute force.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- What does Filebeat watch for?
Filebeat collects data about a file system
- What does Metricbeat record?
Metricbeat records machine metrics or statistics

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address    | Operating System |
|----------|----------|---------------|------------------|
| Jump Box | Gateway  | 10.0.0.1      | Linux            |
| Elk VM   | Server   | 52.149.153.246| Linux            |
| Web 1    | Server   | 10.0.0.6      | Linux            |
| Web 2    | Server   | 10.0.0.7      | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 40.78.99.189

Machines within the network can only be accessed by Jump box.
- Which machine did you allow to access your ELK VM? What was its IP address?
Jumpbox, IP 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses    |
|----------|---------------------|-------------------------|
| Jump Box | Yes/No              | 10.0.0.4 40.78.99.189   |
|  Elk     | No                  | 10.1.0.4 52.149.153.246 |
|  Web 1   | No                  | 10.0.0.6                |
|  Web 2   | No                  | 10.0.0.7                |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-  What is the main advantage of automating configuration with Ansible?_

The main advantage of automating configuration with ansible is it allows automate configurations on multitier apps also the use of ansible playbooks allows to perform multiple tasks at once 

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._ 
- install Docker
- install python3-pip
- install docker python module
- Use more memory
- download and install a dockervelk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ ](/Images/ScreenShot2021-01-02at11.04.46AM.png)

![ ](/Images/ScreenShot2021-01-02at11.03.44AM.png)

![ ](/Images/ScreenShot2021-01-02at11.03.44AM.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring

1. web1 : 10.0.0.6
2. web2 : 10.0.0.7

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed
1. Elk Server - filebeat
2. Web1 - filebeat
3. Web2 - filebeat

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects log files eg
Metricbeat collect machine metrics or statistics eg Uptime
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/filebeat by;
- Update the filebeat-playbook.yml file to include the following commands;filebeat deb download link to download filebeat, install filebeat deb,enable filebeat system module, and copying filebeat config file to /etc/filebeat

![ ](/Images/ScreenShot2021-01-03at12.08.10AM.png)

- Run the playbook, and navigate to 52.149.153.246:5601 to check that the installation worked as expected.

![ ](/Images/ScreenShot2021-01-03at12.15.09AM.png)

Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_

All playbooks are .yml files and they are all located in /etc/ansible

- _Which file do you update to make Ansible run the playbook on a specific machine - Host? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

In order to make ansible run the playbook on a specific machine, you edit the hosts file located in /etc/ansible/hosts where you'll add the specific machine's IP plus the ansible python interpreter under the specific type of server.

![ ](/Images/ScreenShot2021-01-02at12.17.52PM.png)

- _Which URL do you navigate to in order to check that the ELK server is running?

http://52.149.153.246:5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

The screenshot below shows the commands the user will need to run to download playbook, the files, etc

![ ](/Images/ScreenShot2021-01-04at8.49.16PM.png)

After setting up the commands in the playbook yaml file, you run it by using command ansible-playbook followed by the playbook yaml file you just setup eg. after setting up the commands in the filebeat-playbook yaml file, you go ahead and run it by using command ansible-playbook ./filebeat-playbook.yml in the directory the filebeat-playbook.yml file is located 