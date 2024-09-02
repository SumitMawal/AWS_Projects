# VPC - Traffic Flow and Security

## Introduction

This project focused on building a Virtual Private Cloud (VPC) from scratch. This project is a crucial step for anyone looking to master cloud infrastructure. The key tasks accomplished in this project include:

  1.	Creating an **`Amazon VPC`**.
  2.	Creating a **`public subnet`**.
  3.	Setting up an **`internet gateway`**.
  4.	Create a **`route table`**.
  5.	Create a **`security group`**.
  6.	Create a **`Network ACL`** (Network Access Control List).

This project not only enhances my understanding of AWS networking but also prepares me for more advanced cloud projects by providing hands-on experience with essential VPC components.

![image](https://github.com/user-attachments/assets/39f983f2-f639-4d2a-9670-c1f31eaf5ff7)

- ### What is Amazon VPC? 
  Amazon VPC (Virtual Private Cloud) lets you create a logically isolated network in the AWS cloud. It offers control over IP addresses, subnets, route tables, and gateways, enhancing security and flexibility for deploying AWS resources. 

- ### How I used Amazon VPC in this project?
  In this project, I used Amazon VPC to create an isolated network environment. I defined custom subnets, configured route tables, and set up an internet gateway to enable secure communication between my AWS resources and the internet. 

- ### One thing I didn't expect in this project was... 
  One unexpected challenge was configuring the route tables to ensure that public subnets had proper routes to the internet gateway was more intricate than anticipated. This step was crucial to enable internet access for resources in the public subnet. Also configuring Network ACLs to manage traffic flow at the subnet level. Ensuring the correct rules without conflicting with security groups required careful planning and testing.

- ### This project took me... 
  The project took approximately 3 hours to complete. This included setting up the VPC, creating subnets, configuring the internet gateway, fine-tuning security groups and Network ACLs to ensure everything worked seamlessly, and documentation.
 
## Virtual Private Clouds (VPCs) 

Amazon Virtual Private Cloud (VPC) allows you to launch AWS resources in a logically isolated virtual network. You can define your own IP address range, create subnets, and configure route tables and gateways. This setup mimics a traditional network.
 
AWS provides a default VPC in each AWS account to help you quickly get started! This default VPC allows you to launch resources and test AWS services without needing to set up a VPC from scratch. There was already a default VPC in my account as well. 

An IPv4 CIDR block is a group of IP addresses that share a common prefix. CIDR (Classless Inter-Domain Routing) allows for flexible IP address allocation and efficient routing. Ex. 10.0.0.0/24 represents 256 IP addresses from 10.0.0.0 to 10.0.0.255.

![image](https://github.com/user-attachments/assets/2af30726-ca28-44ee-9650-e36d9f12655c)

## Subnets 

A subnet, or subnetwork, is a smaller network within a larger network. You use subnets to group resources with similar access rules and restrictions. 

AWSʼs default VPC includes predefined subnets in each Availability Zone of a Region. If your Region has 3 AZs, you’ll see 3 subnets. These subnets are ready to use, allowing you to quickly launch resources and test services without manual subnet creation. 

I named my subnet Public 1, but that doesn’t automatically make my subnet a public subnet. For a subnet to be considered public, it must have a route to an internet gateway.

![image](https://github.com/user-attachments/assets/2ea6094d-bc9a-40a8-91be-56af674184e8)
 
## Internet gateways 

An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between your VPC and the internet. It supports IPv4 and IPv6 traffic, enabling resources in public subnets to connect to the internet. 

![image](https://github.com/user-attachments/assets/4d897031-3356-4d86-a18b-552766948d14)

Attaching an internet gateway to a VPC means, your instances can access the internet and be accessible to external users! This is crucial for applications that require internet connectivity, like web servers hosting web applications.

![image](https://github.com/user-attachments/assets/f3f55277-03d9-4766-aa54-870dd739fa39)

Even though I've created an Internet Gateway and attached it to your VPC, there's still a step left to go... I still have to tell instances in your public subnet how to get to the internet. This involves setting up route tables to direct traffic from your instances to your internet gateway!

## Route tables 

Route tables are sets of rules in a network that determine where data packets should be directed. Each route specifies a destination IP address, and the next hop (gateway). They ensure efficient data routing within and between networks. 

Routes table are needed to make a subnet public because to let your subnet use an internet gateway, its route table must have a route that directs internet-bound traffic to the internet gateway.

![image](https://github.com/user-attachments/assets/4eabe7b9-318e-46b7-9da2-c572c9c3df1e)

- ### Route destination and target 

  Routes are defined by their destination and target, which mean 
  
   - **Destination:** The IP address range that traffic wants to reach. 
   - **Target:** The road or path that the traffic will have to take to get to its destination.
     
  The route in my route table that directed internet-bound traffic to my internet gateway had a destination 0.0.0.0/0 and a target Internet Gateway (SumitMawal-VPC-IG).
  
  ![image](https://github.com/user-attachments/assets/bd0b533f-9fe2-4dcf-8679-5f2600e2ce67)

## Security groups 

Security groups in AWS act as virtual firewalls for your instances. They control inbound and outbound traffic based on specified rules. You can define allowed IP ranges, ports, and protocols, ensuring secure access to your AWS resources. 

- ### Inbound vs Outbound rules 

  An **`inbound rule`** specifies the allowed incoming traffic to your instances. I configured an inbound rule that include allowing HTTP (port 80) from 0.0.0.0/0, ensuring controlled access to my resources. 


> [!WARNING]
> This wide open access can be risky, exposing your server to potential threats from any location. I configured only for the project's simplicity.


  ![image](https://github.com/user-attachments/assets/158e19a5-3e72-4dc5-a586-b376f9f438a8)

  An **`outbound rule`** specifies the allowed outgoing traffic from your instances. By default, AWS security groups already allow all outbound traffic. So unless you specify. My security group’s outbound rules include allowing all traffic to any destination (0.0.0.0/0), ensuring that my instances can communicate freely with external resources.

  ![image](https://github.com/user-attachments/assets/95dda3bb-e0e1-4b6c-80c3-b5d90473c849)

## Network ACLs 

Think of Network ACLs as traffic cops stationed at every entry and exit point of your subnet, checking each data packet against a table of ACL rules before allowing them through. 
 
![image](https://github.com/user-attachments/assets/eac0f6fe-dde7-4250-bb9c-06ef5b16c0e6)

- ### Security groups vs. network ACLs 

  Network ACLs set broad traffic rules for an entire subnet, like blocking incoming traffic from specific IP ranges or denying outbound traffic to certain ports. Security groups offer granular control, managing access to individual resources by specifying allowed ports and protocols.
 
## Default vs Custom Network ACLs 

- ### Similar to security groups, network ACLs use inbound and outbound rules

  By default, a network ACL's inbound and outbound rules will allow all inbound and outbound traffic, unless customized. 

  ![image](https://github.com/user-attachments/assets/172b4103-dfe9-422e-8f37-90d1de832bb8)

  In contrast, a custom ACLʼs all inbound and outbound traffic are automatically set to denied until you add rules to specify what kind of traffic you'll allow.
 
  ![image](https://github.com/user-attachments/assets/799a7ad2-ebe4-4cec-9c14-ae6065a6d1b8)

## Here's what will happen if you were to set up an EC2 instance in your public subnet and host a web app there:

![image](https://github.com/user-attachments/assets/a3fb6fe6-56c5-4079-8fc9-6a92cdaed6b2)

  **1.  Client/User:** A user enters the URL of your website into their web browser and hits enter.
  
  **2.	Internet Gateway:** The request (in the form of data packets) is sent from the user's browser through the internet and reaches the Internet Gateway (IGW) associated with your VPC, **`Sumit-Mawal-VPC-IG`**.
  
  **3.	VPC:** The Internet Gateway forwards the user's request into your Virtual Private Cloud (VPC), **`Sumit-Mawal-VPC`**.
  
  **4.	Route Table:** Your VPC has a route table for your public subnet (called **`Sumit route table`**), which directs the traffic locally to your EC2 instance hosting the website. The data packets get put on the local route in the route table.
  
  **5.	Network ACL:** While en route to your EC2 instance, the request has to pass through the network ACL associated with your public subnet. The network ACL has an inbound rule to allow all inbound traffic (Inbound Rule 100 allows all inbound traffic i.e. 0.0.0.0/0), so your request is let through.
  
  **6.	Public Subnet:** The request enters your public subnet **`Public 1`**, where your EC2 instance is located.
  
  **7.	Security Group:** The request reaches the security group **`SumitMawal-SecurityGroup`** attached to the EC2 instance. The security group checks its inbound rules to allow or deny the request based on the IP address, protocol, and port. The security group has an inbound rule that allows HTTP traffic (Port 80) from anywhere (0.0.0.0/0).
  
  **8.	EC2 Instance:** The request reaches your EC2 instance hosting the website. The web server on the EC2 instance processes the request and prepares the response.
  
  **9.	Data gets sent back:** The response data from the EC2 instance i.e. website content is sent back to the user. The outbound traffic goes through the security group, public subnet, network ACL, route table, VPC, and Internet Gateway, finally reaching the user's browser, displaying the website content. Amazing work!
