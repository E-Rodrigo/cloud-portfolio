# ☁️ AWS Custom VPC & Automated EC2 Web Server Deployment

## 📌 Project Overview

This project demonstrates the end-to-end provisioning of a custom, isolated network infrastructure on **Amazon Web Services (AWS)** and the deployment of a publicly accessible Linux web server.

Instead of relying on default networking configurations, the entire **Virtual Private Cloud (VPC)** topology—including subnets, internet gateways, routing tables, and stateful firewalls—was architected from scratch to host a bootstrapped **Amazon EC2** instance running the **Apache HTTP Server (`httpd`)**.

## 🏗️ Architecture Overview

```
                        +-------------------------+
                        |      The Internet       |
                        +------------+------------+
                                     |
                                     | (HTTP: 80 / SSH: 22)
                                     v
                        +-------------------------+
                        |    Internet Gateway     |
                        +------------+------------+
                                     |
+------------------------------------|------------------------------------+
| VPC (10.0.0.0/16)                  v                                    |
|                       +-------------------------+                       |
|                       |   Public Route Table    |                       |
|                       |  (0.0.0.0/0 -> igw-id)  |                       |
|                       +------------+------------+                       |
|                                    |                                    |
|        +---------------------------v---------------------------+        |
|        | Public Subnet (10.0.1.0/24)                           |        |
|        |                                                       |        |
|        |   +-----------------------------------------------+   |        |
|        |   | Security Group (Inbound: Ports 80, 22)        |   |        |
|        |   |                                               |   |        |
|        |   |   +---------------------------------------+   |   |        |
|        |   |   | Amazon EC2 Instance (t3.micro)        |   |   |        |
|        |   |   | - OS: Amazon Linux                    |   |   |        |
|        |   |   | - Storage: EBS General Purpose (gp2)  |   |   |        |
|        |   |   | - Service: Apache Web Server (httpd)  |   |   |        |
|        |   |   +---------------------------------------+   |   |        |
|        |   +-----------------------------------------------+   |        |
|        +-------------------------------------------------------+        |
+-------------------------------------------------------------------------+
```

## 🛠️ Technologies & AWS Services Used

| Category | Service / Tool | Purpose in this Project | 
| ----- | ----- | ----- | 
| **Networking** | **Amazon VPC** | Provisioned an isolated virtual network (`10.0.0.0/16`). | 
| **Networking** | **Public Subnet** | Created a dedicated subnet (`10.0.1.0/24`) with auto-assigned public IPv4 addressing. | 
| **Networking** | **Internet Gateway (IGW)** | Enabled bidirectional communication between the VPC and the public internet. | 
| **Networking** | **Route Tables** | Configured custom routing rules (`0.0.0.0/0` pointing to the IGW) associated with the public subnet. | 
| **Security** | **Security Groups** | Configured stateful instance-level firewall rules allowing inbound `HTTP (80)` and `SSH (22)` traffic. | 
| **Compute** | **Amazon EC2** | Deployed a cost-effective `T3` family instance (`t3.micro`) running Amazon Linux. | 
| **Storage** | **Amazon EBS (`gp2`)** | Configured a General Purpose SSD (`gp2`) root volume for consistent boot and I/O performance. | 
| **Administration** | **EC2 Instance Connect** | Established secure, browser-based SSH sessions for server administration and deployment. | 
| **Web Server** | **Apache (`httpd`) & Bash** | Automated web server installation, service initialization, and directory permission management. | 

## 🚀 Step-by-Step Implementation

### 1. Custom Network Provisioning (VPC)

* Created a custom **VPC** with an IPv4 CIDR block of `10.0.0.0/16`.
* Provisioned a **Public Subnet** (`10.0.1.0/24`) inside a single Availability Zone.
* Created and attached an **Internet Gateway (IGW)** to the VPC.
* Configured a **Route Table** with a default route (`0.0.0.0/0`) targeting the IGW, and explicitly associated it with the public subnet.

### 2. Compute, Storage & Firewall Configuration (EC2)

* Launched an **Amazon Linux** EC2 instance (`t3.micro`) inside the custom public subnet with **Auto-assign Public IPv4** enabled.
* Customized the root block device to utilize an **8 GiB General Purpose SSD (`gp2`)** EBS volume.
* Configured a dedicated **Security Group** with the following inbound rules:
  * **SSH (TCP Port 22):** Allowed from `0.0.0.0/0` for remote CLI management via EC2 Instance Connect.
  * **HTTP (TCP Port 80):** Allowed from `0.0.0.0/0` to serve web application traffic publicly.

### 3. Bootstrapping & Automation Script

To automate the web server configuration upon initialization, the following Bash script was designed for the instance's **User Data** execution:

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
chmod -R 777 /var/www/html
```

### 4. Web Application Deployment

Connected to the instance via **EC2 Instance Connect (SSH)** and deployed a custom HTML test page (`projects.html`) into the Apache document root (`/var/www/html/`):

```html
<!DOCTYPE html>
<html>
<body>
<h1>Cloud Infrastructure Project Work</h1>
<p>Automated EC2 & Custom VPC Deployment</p>
</body>
</html>
```

## 🔍 Troubleshooting & Root Cause Analysis (Real-World Scenario)

During the deployment phase, attempting to access the web application via the public IPv4 address initially resulted in a connection failure, and the `/var/www/html/` directory was missing on the filesystem.

### Root Cause

1. Creating the `/var/www/html/` directory manually and assigning `777` permissions was insufficient because the underlying **`httpd` daemon** had not been installed during the initial boot cycle.
2. Without the `httpd` package installed and active on port `80`, the OS kernel rejected incoming HTTP requests regardless of the directory structure.

### Resolution

1. Connected to the instance via **EC2 Instance Connect** and manually executed the package installation while piping the output to `/dev/console` so it remained auditable in the **EC2 System Log**:

   ```bash
   sudo yum install -y httpd | sudo tee /dev/console
   ```

2. Started and enabled the `httpd` systemd service to persist across reboots, and applied the required permissions to the document root:

   ```bash
   sudo systemctl start httpd
   sudo systemctl enable httpd
   sudo chmod -R 777 /var/www/html
   ```

3. Verified local service availability before testing external access:

   ```bash
   sudo systemctl status httpd
   curl http://localhost/projects.html
   ```

## 📂 Repository Structure

```
📦 aws-ec2-vpc-web-deployment
 ┣ 📂 screenshots
 ┃ ┣ 📜 README.md
 ┃ ┣ 🖼️ 01-vpc-and-subnet-creation.jpeg
 ┃ ┣ 🖼️ 02-internet-gateway-attachment.jpeg
 ┃ ┣ 🖼️ 03-route-table-configuration.jpeg
 ┃ ┣ 🖼️ 04-ec2-instance-provisioning.jpeg
 ┃ ┣ 🖼️ 05-ec2-system-log-httpd.jpeg
 ┃ ┗ 🖼️ 06-web-application-live-test.jpeg
 ┗ 📜 README.md
```

## 📸 Proof of Execution (Screenshots)

All step-by-step console verifications and architectural evidence are documented inside the [`./screenshots`](./screenshots/README.md) directory.

## 🧠 Key Takeaways

* **Network Fundamentals:** Understanding how Route Tables, Internet Gateways, and Subnet Associations work together to turn a private subnet into a public one.
* **Defense in Depth:** Controlling traffic flow at the instance level using Security Groups (ports `22` and `80`).
* **Linux System Administration:** Managing services with `systemctl`, handling Linux filesystem permissions (`chmod`), and diagnosing boot-time issues using `/dev/console` and local `curl` tests.
