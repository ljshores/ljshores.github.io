---
layout: post
title:  "Journey to the Cloud with GCP"
date:   2021-02-21
categories: GCP Cloud_Functions Python BigQuery Google_Cloud
---

I hate to admit it, but I’m the girl that when someone starts talking about module versions not matching, spinning up machines, creating tables, and the like, my eyes start to glaze over because I just don’t find that stuff interesting. I just want to dig into the data and not worry about what platform or environment is hosting it. However, as life would have it, I’m working on a project that, if I wanted to move forward with my goals, I needed to think about hosting it somewhere and start thinking about all that data engineering stuff. So, I decided to take the plunge and dive into Google Cloud Platform.

**The Project**  

The short of it is that I wrote some python code that would scrape large amounts of data from the web and store it in csv files. I would then pull those csv files for use into an R shiny script to do some calculations and create a lovely Shiny dashboard. This worked fine on my local computer, but I wanted to be able to move away from my local computer in case I wanted to scale the project up and I also wanted to be able to schedule my python script to run on a daily basis without me having to push run every day.


**Google Cloud Platform**

I decided to try to host my script on GCP because, hey, it’s Google… And also it would be a valuable platform to be familiar with at my job. After doing some research, I decided on which GCP products would help me reach my goal. I would:
* Create an empty BigQuery table to store my data
* Alter my python code so that it writes the scraped data to the BigQuery table, instead of a csv file
* Wrap my python script in a Google Cloud Function
* Use Cloud Schedule and Pub/Sub so that the function could be triggered to run in a serverless way, on a schedule

I’m not going to walk you through every little step, but here are some things you should definitely watch out for that gave me a headache, and a gist of things you must do to achieve the steps I outlined above. 

First of all, everything you do in GCP will need to be tied to a project. This is important because GCP is a paid service depending on if you use resources beyond what they offer for free. So go ahead and create a project.


*Creating a BigQuery Table*

Once you’ve created your project and navigated to BigQuery, you will see that you can create a dataset. You must create a dataset to create tables, so go ahead and do this. Then move forward with creating your table. I created an empty table, where I manually specified my table schema, but you can create a table from Google Cloud Storage, an upload, and other methods.

*Altering the Python Code*
If you want to write a pandas dataframe to a BigQuery table you need to import the bigquery module and use the function client.load_table_from_dataframe()

    from google.cloud import bigquery

    client = bigquery.Client()
    client.load_table_from_dataframe(df, table_id, job_config)

That’s really it. You can look up the function to get details about the arguments that go into it, but this will allow you to load your pandas df to a BigQuery Table.


*Google Cloud Function*
This is how Google describes their cloud functions: a serverless execution environment for building and connecting cloud services. With Cloud Functions you write simple, single-purpose functions that are attached to events emitted from your cloud infrastructure and services. Your function is triggered when an event being watched is fired. Your code executes in a fully managed environment. Sounds good, right? So after navigating to Cloud Functions in your project, you can go ahead and create one.
* Specify what will trigger your function (I used Pub/Sub and this will prompt you to create a bucket in Google Cloud Storage that will be used for staging)
* Specify your runtime (I used Python 3.7)
* You’ll need to edit your python script again by wrapping it in a user defined function. Your function must have the arguments myfun(event, Context) and you will enter the name of your function as your entry point in the GCP console.
* You need to write a requirements.txt file in which you list which modules (and versions) you need for your main.py to run. Note that you may need to include modules that you don’t actually import into your python script. Below, pyarrow was necessary in my requirements file in order to load table from dataframe, but this module is not explicitly imported in my script. Example:
google-cloud-bigquery>=2.7.0
pyarrow>=3.0.0
pandas >=0.25.3
* Bring in your source code. I zipped my main.py and requirements.txt files and uploaded them.
Once all of this is done, you can deploy the function. If that is successful, you can test your function, and once that is done you should see data populated in your BigQuery table!

Getting my function to deploy was definitely not a one and done. I had to figure out a couple of errors, so here are some things to watch out for.
* I kept getting an error: source code string cannot contain null bytes. I realized that some of the things I had in my requirements file was causing this. After removing modules like re, time, datetime,multiprocessing, logging and os, it got rid of this error. I think this is because these are part of the standard library. The ‘pip_download_wheels’ error may also be triggered by issues in the requirements file.
* I already mentioned including modules in your requirements file that some of your other modules may have dependencies on, such as pyarrow
* Make sure your python script is called main.py. It will not work otherwise
* This is basic, but can be a headache if missed…just make sure the spacing in your script is on point

*Schedule the Function to Run*
You can navigate to Cloud Scheduler to create a job. You’ll name it, describe what frequency you want the job to run by providing a string in “unix-cron”  format, and you’ll enter the Pub/Sub topic name that you subscribed to in your function. Bam!

**Wrapping it Up**
I have a confession to make! I never actually made it to the step of scheduling my function to run. My project required that I create two functions and write to two different tables. While one of my function tests worked successfully and did write my data to the table, the other one did not. This is because it continued to have a timeout error. After doing some checking, I realized that a **Google Cloud Function has a max timeout setting of 9 minutes!** This means that if the python script that you’re trying to run in the function takes longer than that, it will never work properly. Considering I’m scraping loads of data, this solution is actually not the solution for me! Too bad I didn’t figure that out before diving so deep into Cloud Functions.

I believe there is a solution for me out there and that it lies in the Google Compute Engine product (spinning up virtual machines….oh no!). So that is what I’ll be exploring next.



