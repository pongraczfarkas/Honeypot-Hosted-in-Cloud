# Honeypot Hosted in Cloud

## Description
This guide details my process of setting up a T-Pot Honeypot server on Azure Cloud. The primary objective of this project was to gain hands-on experience in cybersecurity by deploying and managing a honeypot environment. By implementing T-Pot, I aimed to monitor and analyze potential attacks, thereby enhancing my understanding of threat detection and response. This project emphasizes two crucial aspects of cybersecurity: threat detection and incident response. Using Azure Cloud, I created and configured a virtual machine to host the T-Pot Honeypot server, tracked incoming threats, analyzed the captured data, and documented the findings to improve security measures.

## Resources and Links

- Azure Cloud: [Register](https://azure.microsoft.com/en-us/free/)
- PuTTY: [Download](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
- T-Pot: [Download](https://github.com/telekom-security/tpotce)

## Walkthrough

### Step 1: Create a Virtual Machine on Azure
First, after creating an Azure account, the initial step is to create a Virtual Machine (VM) within the platform.

<div align="center">
    <img src="https://github.com/user-attachments/assets/0d7df1e2-1253-4af2-b4ce-427b33d090e9" alt="Creating a VM"/>
</div>

### Step 2: Create a Resource Group and Configure the VM
I need to create a new resource group, which serves as a logical container. Then, I will set up the closest region to me, give a name to the VM, and purposefully choose Debian 12 x64 from the available images as recommended in the documentation.

<div align="center">
    <img src="https://github.com/user-attachments/assets/b1fbcb26-a143-4005-9cc9-e41a290368c9" alt="Setting up the resource group and VM"/>
</div>

There are additional configurations needed: modify the default setting for the VM size, opting for the 16GB RAM option. Then, I will set up a user account to log into my VM via SSH immediately after it gets provisioned, and save the password in my password manager. Once this configuration is done, I will click Next.

<div align="center">
    <img src="https://github.com/user-attachments/assets/f77bfd56-b077-4628-bb19-43438f1f78b2" alt="Configuring VM details"/>
</div>

### Step 3: Add a New Disk
Following the recommendation, I will add a new disk of 256 GB to the VM.

<div align="center">
    <img src="https://github.com/user-attachments/assets/db34a64a-07cb-474a-954b-222c33087761" alt="Adding a new disk"/>
    <img src="https://github.com/user-attachments/assets/d535ed4c-138e-41cd-a26a-632c5cecea7c" alt="Configuring disk size"/>
</div>

### Step 4: Configure the Network
Next, I will configure the VM's virtual network and assign an IP address to it.

<div align="center">
    <img src="https://github.com/user-attachments/assets/5a08c056-92be-47f9-b4aa-cab64f269f0a" alt="Configuring the network"/>
</div>

### Step 5: Set Up Inbound Rules
To maximize data collection in a short amount of time, I will create an inbound rule to open all ports, even though this contradicts best practices.

<div align="center">
    <img src="https://github.com/user-attachments/assets/2d2e74aa-d8ba-4a72-acea-187e54df285d" alt="Setting inbound rules"/>
    <img src="https://github.com/user-attachments/assets/70e80a44-4f4b-4d6f-8d92-0a25f46fa4d7" alt="Configuring port settings"/>
</div>

### Step 6: SSH into the VM
Now that everything is set up, it is time to SSH into the VM using PuTTY.

<div align="center">
    <img src="https://github.com/user-attachments/assets/788f80e5-ec4f-4918-a8ff-7e3ea002ec0a" alt="SSH into VM"/>
</div>

### Step 7: Update and Upgrade the System
Once logged in, I run `sudo apt update` to update the package lists of the freshly deployed Debian. This step ensures that all packages are up to date.

<div align="center">
    <img src="https://github.com/user-attachments/assets/96452925-9141-482c-bbd3-0fbeafb10437" alt="Updating package lists"/>
</div>

Next, I download the updates using `sudo apt upgrade -y`.

<div align="center">
    <img src="https://github.com/user-attachments/assets/bb9d93fb-88a9-451a-93f8-3a1bc0c97695" alt="Upgrading packages"/>
</div>

### Step 8: Install Git and Clone T-Pot Repository
I install git to clone the T-Pot repository.

<div align="center">
    <img src="https://github.com/user-attachments/assets/916dd84a-5a04-4a35-8893-181a0a8263de" alt="Installing git"/>
    <img src="https://github.com/user-attachments/assets/8eb69340-5649-4cc2-a500-f18793fd5b4d" alt="Cloning T-Pot repository"/>
</div>

### Step 9: Install T-Pot
After downloading, I immediately install T-Pot on my system using `./install.sh`. During the installation, I supply important details such as the web login username and the installation mode for T-Pot. This shell script installs T-Pot with the help of Ansible and Docker. After installation, I terminate the `exim4` and `systemd-resolved` services, which conflict with T-Pot. Following the documentation carefully, I reboot the system.

<div align="center">
    <img src="https://github.com/user-attachments/assets/caa34411-a4e8-4e88-90c7-ea62b1a74bdd" alt="Running install script"/>
    <img src="https://github.com/user-attachments/assets/1719552b-7c42-42d5-956f-5020d838cf8e" alt="Installation process"/>
    <img src="https://github.com/user-attachments/assets/a693bed9-44f8-4034-8516-1ac665086905" alt="Installation progress"/>
    <img src="https://github.com/user-attachments/assets/20a211e1-f2cb-40b3-87fb-756a4b1f5f8e" alt="Installation step"/>
    <img src="https://github.com/user-attachments/assets/586dd264-4fc5-4732-af59-aded50d67635" alt="Completion of installation"/>
    <img src="https://github.com/user-attachments/assets/31ec17df-c6f0-441c-83d7-fd58e2eb77b5" alt="Finalizing installation"/>
</div>

### Step 10: Access T-Pot Web Client
After rebooting the VM and connecting to the web client from my browser, I get these images showing the T-Pot interface.

<div align="center">
    <img src="https://github.com/user-attachments/assets/349724c9-36f6-41c6-9deb-bdb0db03a672" alt="T-Pot web client"/>
    <img src="https://github.com/user-attachments/assets/dc5b00fb-7035-46ac-accd-f29b554647c4" alt="T-Pot dashboard"/>
</div>

### Step 11: Monitoring and Data Collection
Before exploring all possibilities with the software, I leave the VM running for a day to gather data about the attacks.

### Step 12: Analyzing Attack Data
I start the walkthrough with the attack map, which visualizes each attack in real-time from anywhere in the world, displaying statistics and data about the attacks and attackers.

<div align="center">
    <img src="https://github.com/user-attachments/assets/562939d9-96e1-408b-902b-b6b7badddbcb" alt="Attack map"/>
</div>

### Step 13: Investigate an Attacker
I examine a Japanese IP address that has bombarded my VM with attacks. According to [AbuseIPDB](https://abuseipdb.com), this IP is a frequent attacker. The reports often describe it as a source of web application attacks.

<div align="center">
    <img src="https://github.com/user-attachments/assets/91dcc906-05ea-4d0b-af25-3c783c0ae8fc" alt="Investigating an IP address"/>
    <img src="https://github.com/user-attachments/assets/572f4b9f-a1eb-4b5f-8611-4b3de1126ecc" alt="IP details"/>
</div>

### Step 14: Explore CyberChef
CyberChef is an encoder-decoder web

 application that simplifies carrying out cyber operations.

<div align="center">
    <img src="https://github.com/user-attachments/assets/500eb61d-63ea-4931-9f5e-ed36ce115913" alt="CyberChef interface"/>
</div>

### Step 15: Use Elasticvue for Cluster Monitoring
Elasticvue is a GUI tool for Elasticsearch. It helps monitor the cluster, making it easier to add resources if necessary.

<div align="center">
    <img src="https://github.com/user-attachments/assets/8eaa6fb4-11b2-4202-b473-761e9b3952ed" alt="Elasticvue interface"/>
    <img src="https://github.com/user-attachments/assets/311c7162-b2b2-4acd-8bdb-301ac46e585b" alt="Monitoring cluster resources"/>
    <img src="https://github.com/user-attachments/assets/281d1233-03ac-4619-871b-2b69ac180e89" alt="Cluster overview"/>
</div>

I can also search the raw Logstash data in Elasticvue, for example, how many times "admin" appears in the logs.

<div align="center">
    <img src="https://github.com/user-attachments/assets/dc4c15b5-7d2c-4fdf-a1ef-ccae34948c5f" alt="Searching logs"/>
</div>

### Step 16: Analyze Data with Kibana
Kibana's dashboards offer comprehensive views of different honeypots. The T-Pot Dashboard, in particular, consolidates all data.

<div align="center">
    <img src="https://github.com/user-attachments/assets/f6146df1-ada7-4610-a61e-35adfe949d13" alt="Kibana interface"/>
    <img src="https://github.com/user-attachments/assets/8ad79288-ba6b-47ad-8d7c-9fee9d5cb2eb" alt="Kibana dashboard"/>
</div>

The dashboard shows attack types and frequencies, with most attacks being captured by the Honeytrap service. Various diagrams, graphs, and maps present attack statistics.

<div align="center">
    <img src="https://github.com/user-attachments/assets/919ef9b3-3761-488d-963a-7a0579231eed" alt="Attack statistics"/>
</div>

### Step 17: Examine Tagclouds
Tagclouds display frequently used attack parameters, such as usernames and passwords. Larger fonts indicate higher usage. For example, common entries include "root" as the username and "123456" as the password, showing attempts to exploit default configurations.

<div align="center">
    <img src="https://github.com/user-attachments/assets/f28e9f51-9757-4978-bb77-df4e1332842e" alt="Tagcloud analysis"/>
    <img src="https://github.com/user-attachments/assets/e4b29960-2a47-4a2b-abe7-b621646b0c29" alt="Password analysis"/>
</div>

Clicking on a password reveals all users who attempted to use it against my system, with links to detailed attacker information from Talos Intelligence.

<div align="center">
    <img src="https://github.com/user-attachments/assets/6bb85654-98e9-4c39-aade-ddbffda7a8e4" alt="User attempts"/>
    <img src="https://github.com/user-attachments/assets/1a3256fb-fabb-404d-8e90-0a1141ccccb6" alt="Attacker details"/>
</div>

### Step 18: Identify Vulnerabilities
Kibana also highlights attempted exploits against my system. Clicking on a CVE provides detailed information about the attack.

<div align="center">
    <img src="https://github.com/user-attachments/assets/a2e15f2b-edef-4daf-97c8-03930b245b6e" alt="Vulnerability analysis"/>
    <img src="https://github.com/user-attachments/assets/59409373-ad5e-4ce8-b820-7e88218d3b9e" alt="CVE details"/>
</div>

### Step 19: Use Spiderfoot for OSINT
The final tool, Spiderfoot, is used for OSINT attack surface monitoring. By providing an IP address from the attack map, I can gather extensive data about the attacker.

<div align="center">
    <img src="https://github.com/user-attachments/assets/b497b74b-ec3a-420d-b104-2477b44d1993" alt="Spiderfoot interface"/>
</div>

I supplied the second most abusive IP address and started scanning.

<div align="center">
    <img src="https://github.com/user-attachments/assets/c13e927f-1446-45aa-8101-261595d0112f" alt="IP scanning"/>
    <img src="https://github.com/user-attachments/assets/71cf2a7e-93d5-4066-8a9e-85c465df4ba0" alt="Scan in progress"/>
</div>

### Step 20: Review Scan Results
Spiderfoot simplifies data gathering by scanning over 200 types of information simultaneously. Here are the scan results:

<div align="center">
    <img src="https://github.com/user-attachments/assets/ba896985-3127-410f-a1a0-f95e17622ad1" alt="Spiderfoot scan results"/>
    <img src="https://github.com/user-attachments/assets/84a8c723-4e5a-41fc-92e4-ce1e11f35f26" alt="Detailed scan results"/>
    <img src="https://github.com/user-attachments/assets/3ab83b3a-212a-4576-85d2-749867f6d110" alt="Comprehensive data"/>
</div>







