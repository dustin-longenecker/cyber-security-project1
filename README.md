# cyber-security-project1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

**Note**: The following image link needs to be updated. Replace `diagram_filename.png` with the name of your diagram image file.  

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)
![Network Diagram](Images/network-diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the **YAML** file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._
  - [filebeat-playbook](/Ansible-Playbook/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D&mn Vulnerable Web Application.

Load balancing ensures that the application will be highly **available**, in addition to restricting **traffic** to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
- A **load balancer**  is an intelligent network security device that distributes that incoming network traffic across multiple servers. It protects the network from being overwhelmed by incoming traffic.
- The advantage of a jump box is that it is the only machine connected to the public internet. This forces an admin to connect to the jump box before being allowed access to the rest of the network, which can remain private from the public internet.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **logs** and system **data**.
- _TODO: What does Filebeat watch for?_
- Whether you’re collecting from security devices, cloud, containers, hosts, or OT, Filebeat helps you keep the simple things simple by offering a lightweight way to forward and centralize logs and files. (https://www.elastic.co/beats/filebeat)
- _TODO: What does Metricbeat record?_
- Deploy Metricbeat on all your Linux, Windows, and Mac hosts, connect it to Elasticsearch and voila: you get system-level CPU usage, memory, file system, disk IO, and network IO statistics, as well as top-like statistics for every process running on your systems. (https://www.elastic.co/beats/metricbeat)

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name         | Function   | IP Address | Operating System |
|--------------|------------|------------|------------------|
| Jump-Box     | Gateway    | 10.0.0.1   | Linux-Ubuntu     |
| Web-1        | Web Server | 10.0.0.6   | Linux-Ubuntu     |
| Web-2        | Web server | 10.0.0.7   | Linux-Ubuntu     |
| Web-3        | Web Server | 10.0.0.8   | Linux-Ubuntu     |
| Project-VM   | ELK        | 10.1.0.5   | Linux-Ubuntu     |



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_
- Admin IP Adress (My IP address for this project.)

Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
- Jump-Box 10.0.0.1

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | Personal IP Address  |
| Web-1    | No                  | 10.0.0.6             |
| Web-2    | No                  | 10.0.0.7             |
| Web-3    | No                  | 10.0.0.8             |
| ProjectVM| No                  | 10.4.0.1             |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
  -The main advantage of automating configuration with Ansible is that it saves time. Ansible playbooks allow you to install and run applications across multiple virtual machines all at once. It would be extremely time consuming to manually install software on individual machines one at a time. Having one file to troubleshoot for any errors is also another benefit.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
1. **Create a new vNet** in a new region, within your resource group.

2. **Create a Peer Network Connection** between your two vNets.

3. **Create a new VM.** Deploy a new VM into the new vNet with it's own Security Group. This VM will host the ELK server.

4. **Download and configure a container.** Download and configure the `elk-docker` container onto this new VM.

5. **Launch and expose the container.** Launch the `elk-docker` container to start the ELK server.

6. **Implement identity and access management.** Configure your new Security group so you can connect to ELK via HTTP, and view it through the browser.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

**Note**: The following image link needs to be updated. Replace `docker_ps_output.png` with the name of your screenshot image file.  

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
`sudo docker container list -a`

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
- Jump-Box 10.0.0.1
- Web-1 10.0.0.6
- Web-2 10.0.0.7
- Web-3 10.0.0.8
- ProjectVM(ELK) 10.4.0.1

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
- FileBeat
- MetricBeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- FileBeat
  - a lightweight way to forward and centralize logs and files
- MetricBeat
  - a lightweight way to send system and service statistics(CPU usage, memory, file system, disk IO, network IO)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- Copy the Playbook.yml file to `/etc/ansible/roles`.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- Update the `hosts` file to include `10.4.0.1 ansible_python_interpreter=/usr/bin/python3` specfic to the ELK machine.
- _Which URL do you navigate to in order to check that the ELK server is running?
- Run the playbook, and navigate to http://ELKStackPublicIP:5601/app/kibana to check that the installation worked as expected.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
