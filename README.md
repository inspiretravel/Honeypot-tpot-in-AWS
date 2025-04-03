# Project - Honeypot tpot in AWS Cloud Platform

### Objection: 
Setting Up T-Pot Honeypot in AWS EC2 and Integrating with Elastic SIEM 

#Prerequisites

•	AWS Account, Security Group Configuration for AWS EC2, Basic knowledge of Linux commands, Elastic SIEM environment configured
<div></div>


#Skills Learned#


-In-depth understanding of SIEM concepts and hands-on experience with Elastic Security and AWS EC2.

-Proficiency in analyzing and correlating logs from the T-Pot honeypot in Elastic SIEM.

-Ability to identify and investigate attack signatures and threat patterns in AWS-hosted environments.

-Enhanced knowledge of network protocols, intrusion techniques, and security vulnerabilities.

-Development of critical thinking and incident response skills for real-world cybersecurity threats.


#Tools Used#


-Elastic Security (SIEM) for log ingestion, correlation, and threat detection.

-Kibana for visualizing and analyzing honeypot data.

-AWS EC2 for deploying and managing the honeypot environment.

-T-Pot Honeypot Framework for collecting attack telemetry and analyzing adversary behavior.

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

   ![image alt](https://github.com/inspiretravel/Honeypot-tpot-in-AWS/blob/main/AWSnetwork.jpg?raw=true)
   
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

![image alt](https://github.com/inspiretravel/Honeypot-tpot-in-AWS/blob/main/dashboard%20screen.jpg?raw=true)
________________________________________

### Investigation
After several days of VM up, my tpot captured enormous attacks. To conduct my analysus using ELK stack, here is my finding:


![image alt](https://github.com/inspiretravel/Honeypot-tpot-in-AWS/blob/main/dashboard%20screen1.jpg?raw=true)
![image alt](https://github.com/inspiretravel/Honeypot-tpot-in-AWS/blob/main/dashboard%20screen2.jpg?raw=true)
![image alt](https://github.com/inspiretravel/Honeypot-tpot-in-AWS/blob/main/dashboard%20screen3.jpg?raw=true)


Q1.Who are the attackers?
Top 3 attackers is 223.177.160.22, 60.248.96.154, 175.59.74.2. According to talosintelligence, they came from india, taiwan and china.

Q2. What is the common attacks?
The username and password tagclouds show the input attempts used in the brute force attacks. sa is the top username attackers tried to emmurate
And CVE-2006-2369 is the most common attack tactic.


![image alt](https://github.com/inspiretravel/Honeypot-tpot-in-AWS/blob/main/CVE1.jpg?raw=true)


![image alt](https://github.com/inspiretravel/Honeypot-tpot-in-AWS/blob/main/CVE2.jpg?raw=true)

