## Overview

This project demonstrates the use of **Ansible** to automate the deployment and undeployment of an Apache web server on two Ubuntu virtual machines running on Google Cloud Platform (GCP).

Each web server is configured to run on **port 8080** and serves a custom web page with a unique message.

## Project Structure

```
ansible-hw1/
├── deploy.yml
├── undeploy.yml
├── inventory
└── README.md
```

## Environment

- **Control Node:** Ubuntu (Ansible Control)
- **Managed Nodes:**
  - VM1 (webserver1)
  - VM2 (webserver2)
- **Operating System:** Ubuntu 26.04 LTS
- **Automation Tool:** Ansible
- **Web Server:** Apache2

## Files

### `inventory`
Contains the inventory of managed hosts and host-specific variables.

### `deploy.yml`
Deploys and configures Apache on both virtual machines, creates a custom web page, configures Apache to listen on port **8080**, and starts the service.

### `undeploy.yml`
Stops Apache, removes the Apache package, and deletes the deployed web page from both virtual machines.

## Deployment

Run the following command from the control node:

```bash
ansible-playbook -i inventory deploy.yml
```

## Verification

Verify the deployment by accessing each VM:

```bash
curl http://<VM1-IP>:8080
curl http://<VM2-IP>:8080
```

Expected output:

```
Hello World from SJSU-1
Hello World from SJSU-2
```

## Undeployment

Remove the web server resources by running:

```bash
ansible-playbook -i inventory undeploy.yml
```

## Author

**Pranith Varma Pakalapati**

San José State University
