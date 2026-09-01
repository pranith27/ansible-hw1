# Homework #1 – Ansible

Student: Pranith Varma Pakalapati  
University: San José State University

---

## 1. Overview

This project involves automating the deployment and removal of Apache web servers on two Ubuntu virtual machines using Ansible. The virtual machines are hosted on Google Cloud Platform and are configured to serve different webpages on port 8080. The setup includes SSH key-based authentication between the Ansible control node and the managed nodes, enabling passwordless automation.

---

## 2. Project Objectives

The main goals of this project are:

- Set up two Ubuntu virtual machines
- Configure an Ansible control node
- Implement SSH key-based authentication
- Use Ansible to deploy Apache web servers
- Configure Apache to listen on port 8080
- Serve unique webpages on each virtual machine
- Verify the deployment
- Automate the undeployment process

---

## 3. Environment Setup

| Component | Details |
|-----------|---------|
| Cloud Platform | Google Cloud Platform (GCP) |
| Control Node | ansible-control |
| Managed Node 1 | webserver1 (VM1) |
| Managed Node 2 | webserver2 (VM2) |
| Operating System | Ubuntu 26.04 LTS |
| Automation Tool | Ansible |
| Web Server | Apache2 |
| Listening Port | 8080 |

---

## 4. Virtual Machine Configuration

### VM1 (webserver1)

| Property | Value |
|----------|-------|
| Private IP Address | 10.128.0.6 |
| Port | 8080 |
| Webpage Content | Hello World from SJSU-1 |

### VM2 (webserver2)

| Property | Value |
|----------|-------|
| Private IP Address | 10.128.0.5 |
| Port | 8080 |
| Webpage Content | Hello World from SJSU-2 |

Each virtual machine runs Apache on port 8080 and serves a distinct webpage, allowing easy verification of the Ansible configuration.

---

## 5. Repository Structure

```
ansible-hw1/
│
├── deploy.yml
├── undeploy.yml
├── inventory
└── README.md
```

---

## 6. File Descriptions

### inventory

This file contains the list of managed hosts and connection details that Ansible uses to communicate with the virtual machines.

### deploy.yml

The deployment playbook automates the following tasks:

- Install Apache2
- Configure Apache to listen on port 8080
- Create a custom webpage for each VM
- Restart Apache service
- Enable Apache to start on boot

### undeploy.yml

The undeployment playbook handles the removal process by:

- Stopping the Apache service
- Removing the Apache package
- Deleting the custom webpage files

---

## 7. SSH Authentication Setup

SSH key-based authentication was configured to allow passwordless access from the Ansible control node to both managed nodes. This setup enables Ansible to run administrative tasks without manual password entry.

The SSH connection was tested using:

```
ansible all -i inventory -m ping
```

Successful output:

```
vm1 | SUCCESS => {
    "ping": "pong"
}

vm2 | SUCCESS => {
    "ping": "pong"
}
```

---

## 8. Deployment Process

To deploy the Apache web servers, run:

```
ansible-playbook -i inventory deploy.yml
```

This playbook executes the following steps automatically:

1. Installs Apache2 on both VMs
2. Configures Apache to use port 8080
3. Creates the appropriate webpage for each VM
4. Restarts Apache to apply changes
5. Enables Apache to start automatically at system boot

---

## 9. Deployment Verification

Verify the deployment by accessing each VM:

```
curl http://10.128.0.6:8080
```

 output:

```
Hello World from SJSU-1
```

```
curl http://10.128.0.5:8080
```

 output:

```
Hello World from SJSU-2
```

Successful responses confirm that Apache is properly configured and serving the correct content on port 8080.

---

## 10. Undeployment Process

To remove the deployed web servers, run:

```
ansible-playbook -i inventory undeploy.yml
```

This playbook performs the following cleanup tasks:

1. Stops the Apache service
2. Removes the Apache package
3. Deletes the custom webpage files

---

## 11. Undeployment Verification

After undeployment, verify that Apache has been removed:

```
curl http://10.128.0.6:8080
curl http://10.128.0.5:8080
```

 result:

```
curl: (7) Failed to connect...
```

This confirms that Apache is no longer running on either virtual machine.

---

## 12. Requirements Fulfilled

This project addresses all Homework #1 requirements:

- Two virtual machines configured
- Apache web servers deployed using Ansible
- Web servers listening on port 8080
- VM1 serves "Hello World from SJSU-1"
- VM2 serves "Hello World from SJSU-2"
- Deployment and undeployment playbooks included
- Deployment and undeployment verified
- All Ansible scripts uploaded

---

## 13. Repository Contents

The repository includes:

- deploy.yml
- undeploy.yml
- inventory
- README.md

---

## 14. Conclusion

This project successfully demonstrates the use of Ansible for automating the deployment and undeployment of Apache web servers on multiple Ubuntu virtual machines in a cloud environment. The playbooks provide a repeatable, reliable, and automated approach to server management. Verification confirmed that each virtual machine served its designated webpage on port 8080, meeting all project requirements.

---

## 15. Author

Pranith Varma Pakalapati
San José State University
