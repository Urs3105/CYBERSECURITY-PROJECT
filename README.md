## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

![ELK Stack Diagram](https://user-images.githubusercontent.com/79960810/110370133-8d152900-8008-11eb-8ea9-f2a7d15923c6.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file.
  - [Ansible Configuration file](Ansible/ansible.cfg)
  - [Ansible hosts file](Ansible/hosts)
  - [Ansible Playbook Installation Yaml file](Ansible/my-playbook.yml)
  - [Elk Stack Server Installation Yaml file](Ansible/install-elk.yml)
  - [Ansible Filebeat Configuration file](Ansible/Filebeat-config.yml)
  - [Ansible Filebeat Playbook Yaml file](Ansible/Filebeat-playbook.yml)
  - [Ansible Metricbeat Configuration Yaml file](Ansible/Metricbeat-config.yml)
  - [Ansible Metricbeat Playbook Yaml file](Ansible/Metricbeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly ***available/responsive***, in addition to restricting ***access*** to the network.

- What aspect of security do load balancers protect? 

***Answer:*** 
Load balancers are generally located between routers and backend servers, they can detect and stop attacks directed at a server or application, detect and prevent denial-of-service (DoS) and protocol attacks that could cripple a single server.
Some load balancers can hide HTTP error pages or remove server identification headers from HTTP responses, denying attackers additional information about the internal network. 
Load balancers ensure the efficient distribution of incoming network traffic across multiple servers (server pool), receiving and then distributing incoming requests to any available server capable of fulfilling them.

-  What is the advantage of a jump box?_

***Answer:*** 
A jump box is essentially identical to a gateway router. It gives system administrators remote access to the network to provide all the support it needs with very restricted access.The jumpbox sits infront of other machines that are not exposed to the public internet, controlling access to these machines by allowing connections from specific IP addresses.There is just one path in (via SSH)


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

- What does Filebeat watch for?_ 

***Answer:*** 
Filebeat enables analysts to monitor files for suspicious changes. Filebeat can be used to collect, analyze and visualize ELK logs in a single command.Filebeat monitors, generate and organise the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. It is built to collect data about specific files on remote machines and they must be installed on the VMs you want to monitor.


- What does Metricbeat record?_

***Answer:*** 
Metricbeat makes it easy to collect specific information about the machines in the network.
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


**Answer: 
***My Personal IP address***

Machines within the network can only be accessed by ***SSH***.
- Which machine did you allow to access your ELK VM?

***Answer: Jump Box Provisioner (Ansible)***

-  What was its IP address?_

***Answer: 10.0.0.4 (Private IP)***

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses               |
|----------   |---------------------|-------------------------           |
| Jump Box    |     Yes             | Personal IP, 10.0.0.0/16,10.1.0.4  |
| Web1        |     No              | 10.0.0.4 Jump box 10.1.0.4         |
| Web2        |     No              | 10.0.0.4 Jump box, 10.1.0.4        |
| Web3        |     No              | 10.0.0.4 Jump box, 10.1.0.4        |
| ELKServer.  |     Yes             | 10.0.0.4,Personal IP, 10.0.0.0/16  |
|Load Balancer|     Yes             | Personal IP, 10.0.0.0/16, 10.0.0.4 |

## Note
Access control configurations made around the entire network have a network security group created with Inbound and Outbound security rules. The rules being set here allows only my Personal IP address to access the jump box. The security rules that are set within the security group allow the webservers(web-1, web-2, web-3) to communicate with each other and the jump box securely.
An SSH Key was generated and implemented to configure access for the ELK Stack, Jump Box Provisioner, and web servers on the network to prevent brute force attack and to add an extra layer of security.


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?

***Answer:***
         Ansible being an open source automation tool simplifies complex task and increases efficiency.
         Ansible is advantageous because of it being easy to set up and use. Several Virtual Machines could be configured by running an (ansible-playbook).
         No special codes or skills are needed for configuration, a playbook is designed with all tasks that needs to be accomplished and ansible handles the     configuration on the machines after Ansible control node has already been configured. Ansible uses SSH to communicate with the remote hosts as it runs the task in the playbook._

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

- ***Install Docker.io*** - Installs docker to the system

- ***Install Python3-pip*** - Installs Python3-pip to the Docker system

- ***Install Docker python module*** - Installs a Docker module to Python3-pip for the ELK stack

- ***Increase Virtual Memory*** - Before running the elk container, the virtual memory needs to be increased("Use more memory").The virtual memory is increased to 262144 and this will take effect when the system is reloaded

- ***Download and Launch a Docker ELK Container*** - After Docker is installed,download and run the sebp/elk:761 container.The container should be started with these published ports:
  
  ***5601:5601*** (Kibana)
  
  ***9200:9200*** (ElasticSearch)
  
  ***5044:5044*** (Logstash)

- ***Enable Docker system service to boot*** - This task will "enable" the docker system when the system is restarted.


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
![ELK CONFIGURATION](https://user-images.githubusercontent.com/79960810/110042287-cdbc2c00-7d02-11eb-9a01-45726a6d5a37.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring_
Answer:

- ***Web-1 10.0.0.5***

-  ***Web-2 10.0.0.6***

-  ***Web-3 10.0.0.7***

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed_

***Answer: 
- ***Filebeat***
- ***Metricbeat***

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

- ***Filebeat*** 

Enables analysts to monitor files for suspicious changes.

- ***Metricbeat***

Metricbeat makes it easy to collect specific information about the machines in the network.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible/files.
- Update the filebeat-config.yml and metricbeat-config.yml file to include the Private IP address of the ELK Server. The sections output.elasticsearch and setup.kibana of the configuration file.

<img width="600" alt="filebeat-config update" src="https://user-images.githubusercontent.com/79960810/110254938-917d0b80-7f4e-11eb-9089-39c3b728b84b.png">

<img width="533" alt="filebeat-config update(Kibana)" src="https://user-images.githubusercontent.com/79960810/110254966-b07b9d80-7f4e-11eb-9ed5-00fa1967a0ad.png">

- Run the playbook, and navigate to back to the Filebeat installation page on the ELK server GUI to check that the installation worked as expected.This is to confirm if ELK stack is receiving logs.(Kibana)

<img width="693" alt="Filebeat-playbook" src="https://user-images.githubusercontent.com/79960810/110254559-ec156800-7f4c-11eb-9fb0-b82c4135e4ba.png">

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? 

***Answer: [Ansible Filebeat Playbook Yaml file](Ansible/Filebeat-playbook.yml)*** and [Ansible Metricbeat Playbook Yaml file](Ansible/Metricbeat-playbook.yml)

-  Where do you copy it? 

***Answer:/etc/ansible/files***

- _Which file do you update to make Ansible run the playbook on a specific machine? 

***Answer:/etc/ansible/hosts.***

-  How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

***Answer: When the /etc/ansible/hosts file is updated, an additional group is added under a header using brackets [Elk] with an IP address 10.1.0.4 of the ELKserver that Ansible should connect to.***
***With filebeat, the filebeat-config.yaml file is updated with the Private IP of the ELK server to connect the web VM's to the Elk server.*** 

- _Which URL do you navigate to in order to check that the ELK server is running?

***Answer:  http://[your.VM.IP]:5601/app/kibana. Use the public IP address of the ELK server that you created in place of [your.VM.IP]***


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

***Install-Elk***
*  Update the hosts file to include the Private IP address of the ELK Server. The sections output.elasticsearch and setup.kibana of the configuration file.
*  touch and nano install-elk.yml [Elk Stack Server Installation Yaml file](Ansible/install-elk.yml)
*  Run ansible-playbook install-elk.yml (to run the installation)
*  Run curl localhost/setup.php (To confirm success)
*  Navigate to the url ***http://[your.VM.IP]:5601/app/kibana. Use the public IP address of the ELK server that you created in place of [your.VM.IP]***

***Filebeat***
* cd into /etc/ansible directory
* touch filebeat-playbook.yml
* mkdir files
* cp filebeat-config.yml ./files
* nano to update filebeat-playbook.yml [Ansible Filebeat Playbook Yaml file](Ansible/Filebeat-playbook.yml)
* Run ansible-playbook filebeat-playbook.yml
* Navigate to  http://[your.VM.IP]:5601/app/kibana
* Select Module Status and click Check Data. (To confirm if the filebeat installation was a success and that the ELK stack was receiving logs)
* Scroll to the bottom and click on Verify Incoming Data. 

***Metricbeat*** 
* cd into /etc/ansible directory
* touch metricbeat-config.yml
* cp metricbeat-config.yml ./files
* touch metricbeat-playbook.yml
* nano and update metricbeat-playbook.yml [Ansible Metricbeat Installation Playbook Yaml file](Ansible/Metricbeat-playbook.yml)
* Run ansible-playbook metricbeat-playbook.yml
* Navigate to http://[your.VM.IP]:5601/app/kibana
* On the Metricbeat installation page in the ELK server GUI, scroll to  Module Status and click Check Data.(To verify the playbook works as expected)


## References

***https://logz.io/blog/metricbeat-elastic-stack-5-0/***

***https://www.elastic.co/guide/en/beats/filebeat/current/logstash-output.html***

***https://quizlet.com/111255105/ch-7-net-sec-flash-cards/***
