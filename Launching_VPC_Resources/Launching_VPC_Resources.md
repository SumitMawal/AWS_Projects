# Introduction

In this project, I focused on building a robust and secure network infrastructure using Amazon Web Services (AWS). The tasks performed were aimed at creating a well-structured Virtual Private Cloud (VPC) environment. Here is an overview of the key activities:

![image](https://github.com/user-attachments/assets/6a3da456-1f82-4b17-bf16-9fcfa095b41c)

- **VPC Creation Using AWS Wizard:** Utilized the Amazon VPC wizard to expedite the creation of VPCs, ensuring a rapid and efficient setup process.
- **Subnet Creation:** Established both private and public subnets to segregate resources based on their accessibility requirements.
- **Route Table Configuration:** Configured private and public route tables to manage the routing of traffic within the respective subnets.
- **Network ACL Setup:** Implemented private and public Network Access Control Lists (ACLs) to enhance security by controlling inbound and outbound traffic.
- **EC2 Instance Deployment in Public Subnet:** Launched an EC2 instance in the public subnet to facilitate communication with the internet.
- **EC2 Instance Deployment in Private Subnet:** Launched an EC2 instance in the private subnet to ensure secure and isolated operations.
  
This project not only reinforced my understanding of AWS networking services but also highlighted the importance of meticulous planning and execution in creating a secure and efficient network environment.

  > [!NOTE]
  > The below key tasks explained in detail in my “VPC Traffic Flow and Security” project documentation.
  >  1.	Creating an Amazon VPC.
  >  2.	Creating a public subnet.
  >  3.	Setting up an internet gateway.
  >  4.	Create a route table.
  >  5.	Create a security group.
  >  6.	Create a Network ACL (Network Access Control List).

- ### What is Amazon VPC? 
  Amazon VPC (Virtual Private Cloud) lets you launch AWS resources in a logically isolated virtual network. It provides control over your network environment, enhances security, and allows for scalable, flexible infrastructure. 

- ### How I used Amazon VPC in this project? 
  In today’s project, I used VPC to create a private/Public subnet, route table, and network ACL. I launched EC2 instances in both public and private subnets and used the VPC wizard for quick setup, ensuring a secure and efficient network environment.

- ### One thing I didn't expect in this project was... 
  Managing and securing network traffic with custom Network ACLs and route tables can be unexpectedly complex. Balancing security and accessibility, especially for sensitive resources in private subnets, often presents unforeseen challenges. 

- ### This project took me... 
  This project took around 6 hours to complete. Setting up the VPC, creating subnets, configuring route tables and NACLs, and launching EC2 instances required careful planning and testing to ensure everything worked seamlessly, including documentation.

## Private vs Public Subnets 
  A public subnet has a route to an Internet Gateway, allowing resources to access the internet. A private subnet lacks this route, keeping resources isolated from the internet. Public subnets host web servers; private subnets host databases. 

  ![image](https://github.com/user-attachments/assets/fc33ff67-ff00-4ea9-858a-9eb670de623e)

  Private subnets exist to enhance security by isolating sensitive resources from internet. They host databases, application servers, & other backend systems, reducing exposure to external threats & ensuring controlled access through internal networks. 

  Private and public subnets cannot have the same subnet CIDR block.

## A dedicated route table 

  By default, my private subnet is associated with the default routable which was automatically created during VPC creation. 

  I had to set up a new route table because ***NextWork-Sumit-MawalPublicRouteTable*** route table has a route to an internet gateway, and having that route would make ***NextWork-Sumit-Mawal-PrivateSubnet*** public! 

  My private subnet’s route table allows internal traffic within the VPC, such as communication between instances in the same VPC, as I configured a target as Local.
 
  ![image](https://github.com/user-attachments/assets/d27151df-ebe3-4f31-9237-18d2e77c5e88)

## A new network ACL 

  By default, my private subnet is associated with the default Network ACL (NACL), which allows all inbound and outbound traffic. 

  I set up a dedicated network ACL for my private subnet because I want to control traffic more granularly, enhancing security for my private subnet. 

  My new network ACL has two simple inbound and outbound rules - Both denying all inbound and outbound traffic.
 
  ![image](https://github.com/user-attachments/assets/1718aab3-2dbc-4935-ab9c-c5ec50275122)

## Setting Up Direct VM Access

  Directly accessing a (EC2) virtual machine means logging into and managing the operating system or software of the machine as if you were using it in front of you, but over the internet.

- ### SSH is a key method for directly accessing a VM

  SSH, is the protocol we use for secure access to a remote machine. When you connect to the instance, SSH verifies you possess the correct private key corresponding to the public key on the server, ensuring only authorized users can access the instance

- ### To enable direct access, I set up key pairs

  A key pair is primarily used for accessing your EC2 instance securely without going through the AWS Management Console. Instead of the Management Console, you're using SSH (Secure Shell) Access with your key pairs.
 
  ![image](https://github.com/user-attachments/assets/0ee896bb-fda5-4116-806d-a051edd8a000)

  Just like documents can be saved as PDF, DOCX, or TXT for different uses, private keys come in various formats. Not all systems can process every format, so choosing the right one is crucial. My private key's file format was PEM format.

## Launching EC2 Instance

- ### Launching a public server

  I had to change my EC2 instance's networking settings by navigating to Network settings panel, select Edit at the right hand corner.
 
  ![image](https://github.com/user-attachments/assets/738dfa0e-44e1-4361-b8dd-1c39bf2de028)

- ### Launching a private server

  My private server uses a different security group from your public server to enhance security. This allows stricter access controls for sensitive data on the private server, while the public server can have more open rules for external access.
 
  ![image](https://github.com/user-attachments/assets/892f3253-d3cd-4fb7-bf7e-22e3060109c0)

  My private server's security group's source is ***Sumit-Mawal-SecurityGroup*** which means only resources that are part of the ***Sumit-Mawal-SecurityGroup*** (Public) can communicate with my private server instance.

  ![image](https://github.com/user-attachments/assets/1f78f3f7-c84f-4d83-bbe8-db8bcefaf5f3)

- ## Speeding up VPC creation

  I used an alternative way to set up an Amazon VPC! This time, I selected **`VPC and more`** option while creating VPC.

  An AWS VPC resource map visually represents resources within a VPC, such as subnets, route tables, and gateways. It shows relationships and traffic flow, helping you understand and manage your VPC architecture.

  ![image](https://github.com/user-attachments/assets/fefad3f9-43d2-4d0c-b835-83f5d8e8a509)

  Our resource map looks straightforward since we have a nice and simple VPC architecture, but imagine how useful this tool would be for complex VPC setups with many subnets!

### Tips for using the VPC resource map

- **Auto-generate Tag:**

  Name tag auto-generation is a nifty feature that tags all your VPC resources with a name based on what you enter.
  
  If you type in ***`NextWork-SumitMawal`***, all your resources will have that in their name tags, making it super easy to track and manage everything linked to your VPC.
 
  ![image](https://github.com/user-attachments/assets/7a694d21-3356-4d09-85db-9fd8192519d1)

> [!NOTE]
> My new VPC has a CIDR block of 10.0.0.0/16. It can have the same IPv4 CIDR block as my existing VPC because AWS VPCs are isolated by default. There won’t be IP conflicts unless you connect them using VPC peering.
>  
> ![image](https://github.com/user-attachments/assets/701e728a-cbfb-4ae9-8993-a25f69744303)

- **Tenancy:**
  
  Tenancy in AWS refers to the type of hardware your instances run on. You have two main options:
  
  **Default:** Your instances share hardware with other AWS customers. This is the standard option and is cost-effective because you’re sharing resources.
  
  **Dedicated:** Your instances run on hardware that's dedicated to you only. For example, imagine a healthcare company that needs to ensure the highest level of security for patient data. They might choose dedicated tenancy to make sure their servers are completely isolated from other customers, helping them meet compliance standards and keep sensitive information secure. Dedicated does come at a higher cost!

  ![image](https://github.com/user-attachments/assets/18d7b11c-546c-4920-9ac0-43a8afdb18bf)


- **Number of public subnets:**

  When determining the number of public subnets in my VPC, I only had two options: 0 or 2. This was because just one public subnet wouldn’t offer high availability, so AWS doesn't let you create just one! If you need more, you can always add them manually later - you can have up to 200 subnets total in a VPC!
 
  ![image](https://github.com/user-attachments/assets/af924ebe-7051-4463-bb00-973c3d1b1665)

- **Number of private subnets:**
  
  Having more private subnets can help with organizing your resources and isolating them for security purposes, whereas public subnets are limited to ensure manageable exposure to the internet.
 
  ![image](https://github.com/user-attachments/assets/ebed336c-7a4e-4b16-8dac-a09f4fe4a563)

- **NAT Gateways:**
  
  The set up page also offered to create NAT gateways, which let instances in private subnets access the internet for updates and patches, while blocking inbound traffic.

  ![image](https://github.com/user-attachments/assets/3d0caee9-b99c-41ce-b709-e1641c7563da)

  The dollar ($) sign suggests, NAT gateways cost money!

> [!IMPORTANT]
> **Why not Internet Gateway instead of NAT Gateways?**
> 
> Internet gateways let instances in public subnets communicate with the internet both ways i.e. both inbound and outbound traffic.
> 
> Assigning public IP addresses to your instances makes them accessible from the internet, increasing the attack surface. Even with strict security group rules, there's always a risk of misconfiguration or vulnerabilities being exploited. Private subnets are meant to keep your instances isolated from the public internet, so using public IP addresses for instances in private subnets would not be ideal.
>
> That's where NAT gateways come in! Instances in private subnets using a NAT gateway do not need public IP addresses. The NAT gateway handles a translation to a public IP, keeping your instances' private IPs hidden.
 
- **VPC endpoints:**

  Typically, accessing AWS services like S3 from your VPC requires public internet traffic. However, VPC endpoints allow private connections to AWS services, enhancing security and reducing data transfer costs. The S3 Gateway endpoint is the most common, simplifying initial setups by focusing on S3, with other service endpoints added later.

  ![image](https://github.com/user-attachments/assets/36cc9294-7f00-4c94-b200-7e2bb53d15da)

- **DNS options:**

  **Enabling DNS hostnames** allows EC2 instances to have human-readable names, simplifying identification and connection.
   
  **Enabling DNS resolution** ensures AWS translates these hostnames to IP addresses, making it easier to manage instances even if IP addresses change, as hostnames remain consistent.

  ![image](https://github.com/user-attachments/assets/ddf0cfc0-9ed7-4692-a069-1af20a4f3e2b)
