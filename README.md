## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

 - Images/ELK-project-diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

  - Pentest-yml.png or Pentest-yml.rtf

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting access to the network.
- Load balancers protect the servers from getting overwhelmed, either intentionally from a ddos attack or unintentionally from human error or unexpected concentrated access.
- The advantages of a jump box are having one port of entry into the Virtual Network from outside the network. This both insulates and protects the rest of the network while allowing the machine open to the rest of the network to monitor the rest of the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metrics and system files.
- Filesbeat collects data about the file system.
- Metricbeat collects machine metrics, such as uptime.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.0   | Linux            |
| Web-1    | Webserver| 10.1.0.8   | Linux            |
| Web-2    | Webserver| 10.1.0.9   | Linux            |
| Web-3    | Webserver| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.181.120.206

Machines within the network can only be accessed by the jump box machine.
- The ELK server can be accessed only through my own outside machine, which is the same one that can access the jump box machine. Its IP address is 73.181.120.206.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 73.181.120.206       |
| Web-1    | No                  | 104.45.195.34        |
| Web-2    | No                  | 104.45.195.34        |
| Web-3    | No                  | 104.45.195.34        |
| ELK      | Yes                 | 73.181.120.206       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because there is a backup in case anything happened to the ELK server. Further, this system can be duplicated very easily since the yaml files have already been created.

The playbook implements the following tasks:
- increases memory so that the VM has the appropriate resources to run what we need it to
- installs docker
- installs python 3
- installs a docker module using python
- downloads and launches a docker elk container

The following screenshot displays the result of running `Elk_docker.yml` after successfully configuring the ELK instance:
- images/Elk_docker-yml result 

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.1.0.8, 10.1.0.9, 10.1.0.4

We have installed the following Beats on these machines:
- Filebeat, Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects data about the file system. It monitors log files and forwards them to Elasticsearch and Logstash.
- Metricbeat collects machine metrics such as CPU usage, memory, file system, and disk and network I/O.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to /etc/ansible/.
- Update the filebeat-config file to include:
	- Scroll to line #1106 and replace the IP address with the IP address of your ELK machine.
	- Scroll to line #1806 and replace the IP address with the IP address of your ELK machine.
- Run the command ansible-playbook filebeat-playbook.yml
- On your ELK server GUI browser, navigate to the Filebeat installation page (http://[your.VM.IP]:5601/app/kibana) to check that the installation worked as expected.
- If the commands  were successful, the result should look like the Images/FilebeatTest.png