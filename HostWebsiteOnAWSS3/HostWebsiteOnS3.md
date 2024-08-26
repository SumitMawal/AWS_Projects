# Host a Website on Amazon S3
 
## Introduction:

- ### What is amazon S3

  Amazon S3, or Simple Storage Service, is an object storage solution by Amazon. It’s versatile, scalable, and secure, allowing users to    store and retrieve data for various purposes, such as data lakes, websites, mobile apps, backup, and more.

- ### How I used Amazon S3 in this project

  In this project, I utilized Amazon S3 to host the static website.
   ![image](https://github.com/user-attachments/assets/fd1d1410-eea7-47a9-a5cb-8b5426655b9d)

- ### How I Set Up an S3 Bucket:

  Creating an S3 bucket took me less than 5 minute

  The region I picked for my S3 bucket was Asia Pacific (Mumbai) ap-south-1 because I am leaving in Maharashtra, India which is in Asia     Pacific region and also I want to host this site specifically for user from Asia Pacific region.

  An S3 bucket names are globally unique, and all AWS accounts share the namespace. After you create a bucket, no other AWS account in      the entire world can use your bucket's name unless you delete the bucket.

   ![image](https://github.com/user-attachments/assets/61256f14-578d-4f38-852b-a53b38bc2f64)

## Upload Website Files to S3:

- ### Index.html and website/image assets

  I uploaded two files to my S3 bucket - they were 
    1.	Index.html 
    2.	Web-Site-Data-Folder
     
  Both files are necessary for this project as Index.html - To create and design web pages. Web-Site-Data-Folder - This folder having all   files related to website like images, text, etc.
 
   ![image](https://github.com/user-attachments/assets/234200de-7157-46c4-ac89-691c47726eaa)

## Static Website Hosting on S3:

Website hosting that makes your website public on the internet. Storing your HTML file (and the other files for your website) on a web server, so it's accessible online.

To enable website hosting with my S3 bucket, I configured the following settings: Bucket (Created by me)>Properties>Static website hosting>Edit Static web hosting: Enable Hosting type: Host a static website Index document: index.html

## Access Control Lists (ACL):

"An ACL is a set of rules that decides who can get access to a resource." Enabling ACLs in this S3 setup lets you control who can access and do things with the objects (i.e. website files) you upload into your bucket.
 
## Bucket Endpoints:

Once static website is enabled, S3 produces a bucket endpoint URL, which is http://website-project-s3-website-host.s3-website.ap-south-1.amazonaws.com
 
 ![image](https://github.com/user-attachments/assets/008daff8-5a00-4d1a-9810-b75a16392b5a)

## An error:

When I first visited the bucket endpoint URL, I saw "403 Forbidden" error message.

The reason for this error was that my static website is being hosted by S3, but actual HTML/image files I've uploaded are still private. So everyone can see the bucket - but the contents are covered up. I need to set permission of objects to public.
 
![image](https://github.com/user-attachments/assets/efb02fbc-8242-40eb-899a-59a21bdeb7e8)

## Resolution:

- ### Use ACLs to make objects in your S3 bucket public

  To resolve this connection error, I set the permission of the objects to public using ACL.
    1.	Head to the Objects tab
    2.	Select the checkboxes next to your index.html fie and the folder of website assets.
    3.	In the Action dropdown, choose Make public using ACL.
 
   ![image](https://github.com/user-attachments/assets/16849916-62fa-44a4-bf27-6bf8425c7223)
