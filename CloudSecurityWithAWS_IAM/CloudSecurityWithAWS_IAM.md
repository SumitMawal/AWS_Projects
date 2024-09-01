# Cloud Security with AWS IAM
     
<!--
## Table of Content

  Introduction	2
  EC2	3
  What is EC2?	3
  What is EC2 Instance?	3
  Why are I created a new tag? What does this tag mean, how will it be useful later?	3
  IAM	4
  What is AWS IAM?	4
  How I'm using AWS IAM in this project?	4
  IAM Policies	4
  Account Alias	5
  IAM Users and User Groups	6
  Users	6
  User Groups	7
  Testing IAM Policies	8
  Stopping the production instance	8
  Stopping the development instance	8
  IAM Policy Simulator	9 -->

 
## Introduction

In this project, I explored the fundamentals of AWS Identity and Access Management (IAM) and its integration with EC2 services. AWS IAM is crucial for controlling who is authenticated (signed in) and authorized (has permissions) to use your account’s resources.
Throughout this project, I focused on:
  1.	Creating and managing **EC2 instances**
  2.	Developing and applying **IAM Policies**
  3.	Setting up **IAM Users** and **User Groups**
  4.	Configuring an AWS Account **Alias**
     
This hands-on experience provided a comprehensive understanding of securing AWS resources and managing access effectively.
One thing I didn’t expect in this project was how granular and flexible IAM policies could be. The ability to precisely control access at such a detailed level, including specific actions on specific resources, was both surprising and enlightening. 
It took me 2 hours to complete. Most of the time was spent on project documentation.

 ![image](https://github.com/user-attachments/assets/cb0bc791-f337-49c4-88a2-b935abf6746e)

## EC2

### What is EC2?

Amazon EC2 (Elastic Compute Cloud) is a web service that provides resizable compute capacity in the cloud. It allows users to run virtual servers, known as instances, to host applications, manage workloads, and scale resources up or down as needed.

### What is EC2 Instance?

If EC2 is the service that provides virtual computers/servers, each instance is one of those computers/servers that gets produced.
Just like you can choose a computer with more memory or a faster processor when you buy a laptop, with EC2 instances, you can pick a virtual computer that fits what you need for your projects. You can customize your EC2 instance's CPU, memory, storage, and networking capacity and more!

 ![image](https://github.com/user-attachments/assets/a320e5f5-7c20-4663-a8df-76650d124329)

### Why are I created a new tag? What does this tag mean, how will it be useful later?

Tags are like labels you can attach to AWS resources for organization. This tagging helps us with identifying all resources with the same tag at once (they are useful filters), cost allocation, and applying policies based on environment types. 
The tag I’ve used on my EC2 instances is called "Env". The value I’ve assigned for my instances are "Production" and "Development".

![image](https://github.com/user-attachments/assets/c7f70a52-9a5d-41cc-bca9-ab8b69bf1803)
 
## IAM

### What is AWS IAM? 

AWS IAM (Identity & Access Management) enables secure control over AWS services & resources. It allows you to create & manage users, groups, & permissions, ensuring only authorized users can access specific resources, enhancing security & compliance. 

### How I'm using AWS IAM in this project? 

In this project I used AWS Identity and Access Management (IAM) to control who is authenticated (signed in) and authorized (has permissions) to use my account's resources (EC2 instances). 

## IAM Policies 

An IAM policy is a rule for who can do what with your AWS resources. It's all about giving permissions to IAM users, groups, or roles, saying what they can or can't do on certain resources, and when those rules kick in. 
The policy I set up 
For this project, I’ve set up a policy using JSON. 
I’ve created a policy that allows some actions (like starting, stopping, and describing EC2 instances) for instances tagged with "Env = development" while denying the ability to create or delete tags for all instances. 
When creating a JSON policy, you have to define its Effect, Action and Resource. 
  •	**Effect:** This can have two values - either Allow or Deny - to indicate whether the policy allows or denies a certain action. Deny has priority. 
  •	**Action:** A list of the actions that the policy allows or denies. 
  •	**Resource:** Which resources does this policy apply to

![image](https://github.com/user-attachments/assets/d232203a-11cd-45bb-ace4-0dc50eddd0af)

## Account Alias 

Once you on board new users into your AWS account, these new users get access through a unique log-in URL for your account. An Account Alias is friendly name for your AWS account that you can use instead of your account ID to sign in to AWS console. 
Creating an account alias took me less than 5 minute. Now, my new AWS console sign-in URL is ***"https://sumitmawal.signin.aws.amazon.com/console"***.
 
![image](https://github.com/user-attachments/assets/d929bc9a-9f50-45b4-860f-4fc6eb5fe86b)

## IAM Users and User Groups 

### Users 

IAM users are the people that will get access to your resources/AWS account. 

 ![image](https://github.com/user-attachments/assets/68e6b5cc-be66-44e8-8f8d-2181a71ac9a7)

You can share a new user’s sign-in details in two main ways:
•	**Email:** Send the sign-in details directly to the user’s email address. This is secure and ensures the user receives the information privately.
•	**Secure Messaging:** Use a secure messaging platform or tool to share the details, ensuring that the information is encrypted and protected from unauthorized access.

### User Groups 

An IAM user group is a collection/folder of IAM users. It allows you to manage permissions for all the users in your group at the same time by attaching policies to the group rather than individual users.
Attaching an IAM policy to a user group grants all members of that group the permissions defined in the policy. This simplifies permissions management, ensuring consistent access control across users and reducing the need for individual policy.
 
![image](https://github.com/user-attachments/assets/0c5f5dcd-e679-4822-9e35-2ce511a24993)

Once I logged in as my IAM user, I noticed that some of my dashboard panels are showing Access denied already!

![image](https://github.com/user-attachments/assets/8c7374ad-60ea-431c-9eb3-25d13d93f914)

## Testing IAM Policies 

I tested my IAM policy by attempting to stop both EC2 instances with the new user (dev-sumit-mawal). I observed that I couldn’t stop the Production EC2 but could stop the Development EC2, as I granted the new user access only to the Development EC2. 

### Stopping the production instance 

When I tried to stop the production instance, red banner pop up that tells I've failed to stop this instance. It's because I am not authorized! I don't have permission to stop any instance with the production tag.

![image](https://github.com/user-attachments/assets/933f0d5b-fd25-49be-b547-674b7c21455e)

### Stopping the development instance 

Next, when I tried to stop the development instance, it stopped successfully. This is because I have permission to stop any instance with the Development tag under the ***DevEnvironmentPolicy***.
 
![image](https://github.com/user-attachments/assets/9bd24a2f-8301-48a3-9330-e93e0fbfeaa2)

## IAM Policy Simulator

Have you noticed that to test out the effectiveness of our policy, we had to shut down the instance? In the real world, you might not want to actually shut down your EC2 instances just to test your custom IAM policy (this could get pretty disruptive).
The IAM Policy Simulator lets you test and validate your policies without affecting your actual AWS resources. In your IAM dashboard, look for the Policy Simulator link under the Tools panel. (login with main AWS account)

![image](https://github.com/user-attachments/assets/eb5ee63c-c4ce-45ea-a197-0566b392f65e)

![image](https://github.com/user-attachments/assets/4f74bdf0-13e0-45a1-9742-856255970f37)
