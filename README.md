# Honeypot Hosted in Cloud

## Description
This guide details my process of setting up a T-Pot Honeypot server on Azure Cloud. The primary objective of this project was to gain hands-on experience in cybersecurity by deploying and managing a honeypot environment. By implementing T-Pot, I aimed to monitor and analyze potential attacks, enhancing my understanding of threat detection and response. This project emphasizes two crucial aspects of cybersecurity: threat detection and incident response. Using Azure Cloud, I will create and configure a virtual machine to host the T-Pot Honeypot server, track incoming threats, analyze the captured data, and document the findings to improve security measures.

## Resources and links

- Azure Cloud: [Register](https://azure.microsoft.com/en-us/free/)
- PuTTY: [Download](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
- T-Pot: [Download](https://github.com/telekom-security/tpotce)

## Walkthrough
First step after creating an Azure account is to create a Virtual Machine within the platform

<div align="center">
    <img src="https://github.com/user-attachments/assets/0d7df1e2-1253-4af2-b4ce-427b33d090e9" alt="image"/>
</div>
<div align="center">
    <img src="https://github.com/user-attachments/assets/b1fbcb26-a143-4005-9cc9-e41a290368c9" alt="image"/>
</div>

I need to create a new resource group, which is going to serve as a logical container. Then I will set up the closest region to me, give a name to the VM and purposefully choose Debian 12 x64 from the available images because it was recommended in the documentation.

<div align="center">
    <img src="https://github.com/user-attachments/assets/f77bfd56-b077-4628-bb19-43438f1f78b2" alt="image"/>
</div>

There are still more to do on this window: I will modify the default setting on the size of the VM and I will choose the option with 16GB of RAM. Then I will set up a user account to be able to log into my VM with the help of SSH immediately after it gets provisioned. I will also save the password to my password manager. As this window is done, I will click Next.

<div align="center">
    <img src="https://github.com/user-attachments/assets/31404f0b-b968-4054-8424-21f0cb535437" alt="image"/>
</div>

Here I will add a new disk, which will be (following the recommendation again) 256 GB. 

<div align="center">
    <img src="https://github.com/user-attachments/assets/db34a64a-07cb-474a-954b-222c33087761" alt="image"/>
    <img src="https://github.com/user-attachments/assets/d535ed4c-138e-41cd-a26a-632c5cecea7c" alt="image"/>
</div>

I will then give names to the VM's virtual network and will give IP address to it.

<div align="center">
    <img src="https://github.com/user-attachments/assets/5a08c056-92be-47f9-b4aa-cab64f269f0a" alt="image"/>
</div>

The next step is also very important. I will make an inbound rule which will open all the ports. Although this goes completely against the best practices, I want as much data to be collected as possible in a short amount of time.

<div align="center">
    <img src="https://github.com/user-attachments/assets/2d2e74aa-d8ba-4a72-acea-187e54df285d" alt="image"/>
    <img src="https://github.com/user-attachments/assets/70e80a44-4f4b-4d6f-8d92-0a25f46fa4d7" alt="image"/>
</div>

Now that I have set up everything, it is time to SSH into my machine via PuttY.

<div align="center">
    <img src="https://github.com/user-attachments/assets/788f80e5-ec4f-4918-a8ff-7e3ea002ec0a" alt="image"/>
</div>

Then I ran `sudo apt update` to update the package lists of my freshly deployed Debian. Do not forget to do these steps with every freshly installed operating system. It could be possible that there are updates to them and their packages.

<div align="center">
    <img src="https://github.com/user-attachments/assets/96452925-9141-482c" alt="image"/>
</div>

Now that we have an updated package list, let's download the updates `sudo apt upgrade -y`

<div align="center">
    <img src="https://github.com/user-attachments/assets/bb9d93fb-88a9-451a-93f8-3a1bc0c97695" alt="image"/>
</div>

I install git here so I could clone the T-Pot repository.

<div align="center">
    <img src="https://github.com/user-attachments/assets/916dd84a-5a04-4a35-8893-181a0a8263de" alt="image"/>
    <img src="https://github.com/user-attachments/assets/8eb69340-5649-4cc2-a500-f18793fd5b4d" alt="image"/>
</div>

After I finished the download, I went to immediately install T-Pot on my system with the command `.install sudo apt upgrade -y. I will add a bunch of important stuff to the application, like what my username will be on the web login, what mode do I want to install T-Pot in etc.

<div align="center">
    <img src="https://github.com/user-attachments/assets/1719552b-7c42-42d5-956f-5020d838cf8e" alt="image"/>
    <img src="https://github.com/user-attachments/assets/a693bed9-44f8-4034-8516-1ac665086905" alt="image"/>
    <img src="https://github.com/user-attachments/assets/20a211e1-f2cb-40b3-87fb-756a4b1f5f8e" alt="image"/>
    <img src="https://github.com/user-attachments/assets/586dd264-4fc5-4732-af59-aded50d67635" alt="image"/>
    <img src="https://github.com/user-attachments/assets/31ec17df-c6f0-441c-83d7-fd58e2eb77b5" alt="image"/>
    <img src="https://github.com/user-attachments/assets/349724c9-36f6-41c6-9deb-bdb0db03a672" alt="image"/>
    <img src="https://github.com/user-attachments/assets/dc5b00fb-7035-46ac-accd-f29b554647c4" alt="image"/>
    <img src="https://github.com/user-attachments/assets/562939d9-96e1-408b-902b-b6b7badddbcb" alt="image"/>
    <img src="https://github.com/user-attachments/assets/91dcc906-05ea-4d0b-af25-3c783c0ae8fc" alt="image"/>
    <img src="https://github.com/user-attachments/assets/572f4b9f-a1eb-4b5f-8611-4b3de1126ecc" alt="image"/>
    <img src="https://github.com/user-attachments/assets/8eaa6fb4-11b2-4202-b473-761e9b3952ed" alt="image"/>
    <img src="https://github.com/user-attachments/assets/311c7162-b2b2-4acd-8bdb-301ac46e585b" alt="image"/>
    <img src="https://github.com/user-attachments/assets/281d1233-03ac-4619-871b-2b69ac180e89" alt="image"/>
    <img src="https://github.com/user-attachments/assets/dc4c15b5-7d2c-4fdf-a1ef-ccae34948c5f" alt="image"/>
    <img src="https://github.com/user-attachments/assets/f6146df1-ada7-4610-a61e-35adfe949d13" alt="image"/>
    <img src="https://github.com/user-attachments/assets/8ad79288-ba6b-47ad-8d7c-9fee9d5cb2eb" alt="image"/>
    <img src="https://github.com/user-attachments/assets/919ef9b3-3761-488d-963a-7a0579231eed" alt="image"/>
    <img src="https://github.com/user-attachments/assets/f28e9f51-9757-4978-bb77-df4e1332842e" alt="image"/>
    <img src="https://github.com/user-attachments/assets/e4b29960-2a47-4a2b-abe7-b621646b0c29" alt="image"/>
    <img src="https://github.com/user-attachments/assets/6bb85654-98e9-4c39-aade-ddbffda7a8e4" alt="image"/>
    <img src="https://github.com/user-attachments/assets/1a3256fb-fabb-404d-8e90-0a1141ccccb6" alt="image"/>
    <img src="https://github.com/user-attachments/assets/a2e15f2b-edef-4daf-97c8-03930b245b6e" alt="image"/>
    <img src="https://github.com/user-attachments/assets/59409373-ad5e-4ce8-b820-7e88218d3b9e" alt="image"/>
    <img src="https://github.com/user-attachments/assets/b497b74b-ec3a-420d-b104-2477b44d1993" alt="image"/>
    <img src="https://github.com/user-attachments/assets/c13e927f-1446-45aa-8101-261595d0112f" alt="image"/>
    <img src="https://github.com/user-attachments/assets/71cf2a7e-93d5-4066-8a9e-85c465df4ba0" alt="image"/>
    <img src="https://github.com/user-attachments/assets/ba896985-3127-410f-a1a0-f95e17622ad1" alt="image"/>
    <img src="https://github.com/user-attachments/assets/84a8c723-4e5a-41fc-92e4-ce1e11f35f26" alt="image"/>
    <img src="https://github.com/user-attachments/assets/3ab83b3a-212a-4576-85d2-749867f6d110" alt="image"/>
</div>







