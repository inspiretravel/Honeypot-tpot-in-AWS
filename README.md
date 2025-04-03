# Project - Honeypot tpot in AWS Cloud Platform

### Objection: 
Setting Up T-Pot Honeypot in AWS EC2 and Integrating with Elastic SIEM 

#Prerequisites

•	AWS Account, Security Group Configuration for AWS EC2, Basic knowledge of Linux commands, Elastic SIEM environment configured
________________________________________
Step 1: Launch an AWS EC2 Instance
1.	Log in to the AWS Management Console.
2.	Navigate to EC2 Dashboard and click Launch Instance.
3.	Choose an Ubuntu 22.04 LTS AMI (recommended for T-Pot).
4.	Select an instance type:
Minimum recommended: t3.medium (2 vCPUs, 4GB RAM) , Preferred for better performance: t3.large (2 vCPUs, 8GB RAM)
5.	Configure security groups:
   
    -Allow SSH (Port 22) for your IP
  	
    -Allow required honeypot ports (e.g., 80, 443, 22, 23, 3389, etc.)

    -Allow outbound access for updates.
   
7.	Set up key pair for SSH authentication.
8.	Click Launch Instance and wait for it to be available.
<div></div><div></div>
________________________________________

Step 2: Install T-Pot on EC2
1.	SSH into the EC2 instance:
ssh -i your-key.pem ubuntu@your-ec2-public-ip
2.	Update system packages:
sudo apt update && sudo apt upgrade -y
3.	Install required dependencies:
sudo apt install -y git curl
4.	Download and install T-Pot:
5.	cd /opt
6.	git clone https://github.com/telekom-security/tpotce.git
7.	cd tpotce/iso/installer/
sudo ./install.sh
8.	Follow the interactive prompts:

    -Choose installation type (Standard, Minimal, etc.)

    -Set up admin credentials

9.	Reboot the system after installation:
sudo reboot
________________________________________

Step 3: Verify T-Pot is Running
1.	SSH back into the instance after reboot.
2.	Check running containers:
sudo docker ps
3.	Access T-Pot Web UI:

-Open http://your-ec2-public-ip:64297

-Log in using the admin credentials set during installation.
________________________________________
