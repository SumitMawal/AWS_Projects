# Visualize Data with QuickSight

## Introduction

- ### What is Amazon QuickSight? 
  Amazon QuickSight is a powerful business intelligence tool. It lets you create interactive dashboards, analyse data, and share insights. 

- ### How I used Amazon QuickSight in this project?
  In this project I used Amazon QuickSight to analyse a huge dataset of Netflix shows and movies to create a dashboard that extracts all the juicy insights. 

- ### What is one thing that didn't expect in this project? 
  I didn't expect that even if I am not familiar with data analysis, still I manage to make insightful dashboard with Amazon QuickSight. It is really designed to be beginner friendly. 

- ### How much time it take to complete this project?
  To complete this project for me it took about 2 hour.
 

## How I Set Up an S3 Bucket

Creating an S3 bucket took me less than 5 minute
The region I picked for my S3 bucket was Asia Pacific (Mumbai) ap-south-1 because I am leaving in Maharashtra, India which is in Asia Pacific region and also I want to host this site specifically for user from Asia Pacific region.
An S3 bucket names are globally unique, and all AWS accounts share the namespace. After you create a bucket, no other AWS account in the entire world can use your bucket's name unless you delete the bucket.

![image](https://github.com/user-attachments/assets/d5c78d57-f65b-44e8-9635-e2b1dc1ba5fe)


## Upload project files into S3 

S3 is used in this project to store two files, which are mentioned below, 
  1.	manifest.json 
  2.	netflix_titles.csv
     
I edited the manifest.json file by replacing the S3 URL of dataset (netflix_titles.csv). It’s important to edit this file because we need to connect our dataset to Amazon QuickSight.

![Copy_S3_URL_for_CSV](https://github.com/user-attachments/assets/4192194a-3ce9-486c-9c2e-bb66427969c6)


## Create QuickSight account 

Creating a QuickSight account cost no money. QuickSight comes with a free trial so you won't be charged for this project. Make sure you ***uncheck the Add Paginated Reports option***. So your AWS account doesn't get charged! 
Creating an QuickSight account took me around 5 minute.

![QuickSite_Accout_Created](https://github.com/user-attachments/assets/f7246db0-4c91-4965-88ef-b2526c3f847a)


## Download the Dataset 

I connected the S3 bucket to QuickSight by visiting Datasets option which is at left hand navigation bar. 

The ***manifest.json*** file is like a map that tells Amazon QuickSight where your data lives and how to read your data. Manifest.json tells QuickSight what your dataset looks like, so QuickSight knows how to understand the data and show it in charts or graphs.

![Dataset_Pannel](https://github.com/user-attachments/assets/383055b1-4b05-4c44-a36e-69088f49c420)


## My first visualization 

To create visualizations on QuickSight, I drag fields into the graph to create visualisations. We can see on the left hand panel that dataset's fields are already imported. We can sort, filter, and customise our data top create visualisations. We can also experiment with different types of graphs like bar charts, pie charts, line graphs, etc. 

The chart/graph shown here is a breakdown on the year that these Netflix-featured TV shows and movies were released. Also breakdown of TV shows vs movies for every year. 

I created this graph by dragging and dropping - release_year and type field from dataset.

 ![Visulization1](https://github.com/user-attachments/assets/5e2aeb43-6f4c-4207-8801-9061422862db)


## Using filters 

Filters are essential tools in various contexts, providing a way to selectively process or manipulate data. 

This visualization is a breakdown of TV shows/movies for each release year. Also showed same in table format. Here I added a filter to date_added field to find, on what day did Netflix add the largest number of movies/TV shows to their catalogue. Moreover to find how many 'Action & Adventure', 'TV Comedies', or 'Thrillers' were released on 2015 or after.

 ![Dashboard](https://github.com/user-attachments/assets/b7cf2332-6aef-4e5a-b971-0095d4e8a9f9)

 
## Setting up a dashboard 

As a finishing touch, I edited the titles in each charts so that anyone can understand them at a glance. 

Did you know you could export your dashboard as PDF too? I did this by clicking on the top right hand corner, select the ***Expert icon***. Then select ***Generate PDFs***. Wait for the PDF to be ready, then select ***Download*** when you see that green banner pop up!

![Final_Dashboard](https://github.com/user-attachments/assets/e445cbca-5eaf-4355-8eb9-268baaa23457)
