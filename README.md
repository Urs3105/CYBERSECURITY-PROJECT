## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

<img width="1040" alt="ELK Stack Deployment" src="https://user-images.githubusercontent.com/79960810/110149954-e4629180-7d9b-11eb-872c-9526df0cdbff.png">

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file.
  - [Ansible Configuration file](Ansible/ansible.cfg)
  - [Ansible hosts file](Ansible/hosts)
  - [Ansible Playbook Installation Yaml file](Ansible/my-playbook.yml)
  - [Elk Stack Server Installation Yaml file](Ansible/install-elk.yml)
  - [Ansible Filebeat Configuration file](Ansible/Filebeat-config.yml)
  - [Ansible Filebeat Playbook Yaml file](Ansible/Filebeat-playbook.yml)
  - [Ansible Metricbeat Configuration Yaml file](Ansible/Metricbeat-config.yml)
  - [Ansible Metricbeat Installation Playbook Yaml file](Ansible/Metricbeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available/responsive, in addition to restricting access to the network.
- _TODO: What aspect of security do load balancers protect? 
Answer: Load Balancers defends a system/organisation from DDoS attacks by shifting attack traffic from the server to a public cloud provider.
        Load balancers ensure the efficient distribution of incoming network traffic across multiple servers
-  What is the advantage of a jump box?_
Answer: A jump box is essentially identical to a gateway router. It gives system administrators remote access to the network to provide all the support it needs with very restricted access.The jumpbox sits infront of other machines that are not exposed to the public internet, controlling access to these machines by allowing connections from specific IP addresses.There is just one path in (via SSH)

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

- _TODO: What does Filebeat watch for?_ 
-Answer: Filebeat enables analysts to monitor files for suspicious changes. Filebeat can be used to collect, analyze and visualize ELK logs in a single command.Filebeat monitors, generate and organise the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. is built to collect data about specific files on remote machines and must be installed on the VMs you want to monitor.

- _TODO: What does Metricbeat record?_
Answer: Metricbeat makes it easy to collect specific information about the machines in the network.
Metricbeat gathers a variety of metrics and statistics from a server(operating system and other services on the server). It then ships them to an output destination of choice. It could be to Elasticsearch,logstash or any other data processing platforms.
The configuration details of each machine may be found below.

_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name        | Function                   | IP Address    | Operating System        |
|----------   |----------------------------|------------   |------------------       |
| Jump Box    | Gateway                    | 10.0.0.4      | Linux (Ubuntu 18.04 LTS)|
| Web1        | Webserver                  | 10.0.0.5      | Linux (Ubuntu 18.04 LTS)|
| Web2        | Webserver                  | 10.0.0.6      | Linux (Ubuntu 18.04 LTS)|
| Web3        | Webserver                  | 10.0.0.7      | Linux (Ubuntu 18.04 LTS)|
| ELKServer.  | Logs Data                  | 10.1.0.4      | Linux (Ubuntu 18.04 LTS)|
|Load Balancer| Distributes Network Traffic| 52.247.213.224| Linux (Ubuntu 18.04 LTS)|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- _TODO: My Personal IP address

Machines within the network can only be accessed by _SSH____.
- _TODO: Which machine did you allow to access your ELK VM?
Answer: Jump Box Provisioner (Ansible)

-  What was its IP address?_
Answer: 10.0.0.4 (Private IP)

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses               |
|----------   |---------------------|-------------------------           |
| Jump Box    |     Yes             | Personal IP, 10.0.0.0/16,10.1.0.4  |
| Web1        |     No              | 10.0.0.4 Jumpbox , 10.1.0.4        |
| Web2        |     No              | 10.0.0.4 Jump box, 10.1.0.4        |
| Web3        |     No              | 10.0.0.4 Jump box, 10.1.0.4        |
| ELKServer.  |     Yes             | 10.0.0.4/Personal IP Address.      |
|Load Balancer|     Yes             | Personal IP, 10.0.0.0/16

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?
***Answer:***
         Ansible being an open source automation tool simplifies complex task and increases efficiency.
         Ansible is advantageous because of it being easy to set up and use. Several Virtual Machines could be configured by running a script(Ansible playbook)
         No special codes or skills were needed for the configuration, a playbook was designed and Ansible handled the configuration on the machines after Ansible          control node has already been configured. Ansible used SSH to communicate with the remote hosts and run the task in the playbook._

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
*** Install docker.io
*** Install pip3
*** Install docker python modules
*** Increase virtual memory
*** Download and launch docker elk container




The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
![ELK CONFIGURATION](https://user-images.githubusercontent.com/79960810/110042287-cdbc2c00-7d02-11eb-9a01-45726a6d5a37.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
- ***Answer:

- ***Web-1 10.0.0.5***

-  ***Web-2 10.0.0.6***

-  ***Web-3 10.0.0.7***

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
- ***Answer: 
- ***Filebeat***
- ***Metricbeat***

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- ***Answer:*** 

- ***Filebeat*** enables analysts to monitor files for suspicious changes.

- ***Metricbeat***
Metricbeat makes it easy to collect specific information about the machines in the network.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files.
- Update the filebeat-config.yml file to include the Private IP address of the ELK Server. The sections output.elasticsearch and setup.kibana of the configuration file.
- Run the playbook, and navigate to back to the Filebeat installation page on the ELK server GUI to check that the installation worked as expected.This is to confirm if ELK stack is receiving logs.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? (Insert configfile) filebeat-playbook.yml file
-  Where do you copy it? /etc/ansible
- _Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible/hosts file.
-  How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
 When the /etc/ansible/hosts file is updated, an additional group is added under a header using brackets [Elk] with an IP address 10.1.0.4 of the ELKserver that Ansible should connect to.
- _Which URL do you navigate to in order to check that the ELK server is running?
 Answer:  http://[your.VM.IP]:5601/app/kibana. Use the public IP address of the ELK server that you created in place of [your.VM.IP]
 
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
* ssh sysadmin@jumpboxprovisioner(Public IP)
* sudo apt install docker.io - A Docker allows a user to run Linux containers on any local machine or server.
* sudo systemctl start docker
* sudo systemctl status docker
* sudo docker pull cyberxsecurity/ansible - This will downloader a container fro the cyberxsecurity docker repository.
* sudo docker container list -a - This will list all of the containers on the system.(Those that are up and inactive containers)
* sudo docker start container. (The unique name of the container)
* sudo docker ps (To check the current status of the container)
* sudo docker attach container (Container name). This will give you a shell on the specific container
* cd /etc/ansible 
* nano hosts (Update the file with Private IP addresses of webservers that needs ansible playbook run on)
* ansible -m ping all ( This pings all of the webservers listed in the hosts file)
* ansible-playbook my-playbook.yml ( The ansible-playbook will run the contents of the desired named yml file)
