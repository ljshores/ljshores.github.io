---
layout: post
title:  "Deeper into the Cloud: Using VMs on Google Compute Engine to Run a Python Script"
date:   2021-02-28
categories: GCP Compute_Engine Python Google_Cloud
---

If you read my last post, you know that I tried to use Cloud Functions on Google Cloud Platform to run a python script that would scrape data from the web and write it to a BigQuery table. Unfortunately, that solution turned out not to work for my purposes, because Cloud Functions have a timeout at nine minutes, and my scraper would need to run for longer than that. So I decided to host and run my script on a Compute Engine VM (virtual machine) instance. I’ll outline how I did this and some things to watch out for below.  

Using the project that I had created before from the last post, I already had my BigQuery table set up and ready to go. I just needed to:
   * Create a VM instance and set up the environment for my purposes
   * Get my python code on the instance
   * Automatically trigger the python script to run upon starting the VM
   * Create a schedule to start and stop the VM  


**Creating a Google Cloud VM**  

Google’s Compute Engine product allows you to spin up a virtual machine so that you can do all the things you would do on your local computer, on the cloud. GCE makes this very easy to do. In your specific project navigate to Compute Engine, and in the top you should see the option to “Create Instance”. Name your vm instance. The default settings should be fine to use; just change the region to be the one closest to you and pay attention to the machine configuration series and machine type. These settings determine how much compute and memory are allocated to your instance, and thus affect your cost of using the VM. The cheapest option would be to use the N1 series, f1 micro machine type. That’s it for now. Hit create and you now have a vm instance.

**Get My Code on the Instance**  

You now have an instance….now what? Well, as I said before you should think of this as giving you the functionality of your local computer. The main difference is that you don’t have a pretty interface to navigate around and click on stuff to do what you want to do. You will need to connect by opening an SSH window. This will allow you to do everything you need by using linux commands. Again, this is not my forte. But, I’ll discuss some useful commands that will allow you to get stuff done.  

When your SSH window is open, you will notice that on the upper right hand side there is a gear. There you’ll have the option to upload files, so upload your python script as well as your requirements.txt (this should contain all the python modules that you will need to run your script, the same as the exercise we did for trying to get Cloud Functions up and running). You can check that your files are on the instance by typing the command below, which will give you a list of the files in the directory you are currently in.  

    ls -l

Now you have your necessary files, but your VM is a bank slate. You will need to install python and pip so that you can install packages.  

    sudo apt-get install python3.7
    sudo apt-get install python3-pip
    sudo curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
    sudo python3 get-pip.py

You can test to make sure you have python installed by typing python3 (use quit() to exit python). Now that python and pip are installed, you can install your required modules on the vm.  

    pip install -r requirements.txt

This is it! You can now run your python script in the SSH window and when it’s done you can check your BigQuery table, and you should see results there.  

    python3 mypythonscript.py 

Note: if you need to open and/or edit your files on the vm, you can use nano text editor.  

    nano mypythonscript.py


**Automatically Run the Python Script Upon Starting the VM**  
  
As mentioned before, GCP is not free. For my purpose of running a python script once a day, I didn’t need my VM to be running all during the day, incurring costs. So my goal was to schedule the VM to start every day, have the python script run, and then shut the VM down. Luckily, GCE has the option to add a “startup-script” to your VM. It’s a script that tells the VM to perform certain actions every time it starts up. I’ve seen examples of the startup script being used to update software and other tasks like that, but all we want to do is to literally just run the python script. Google makes this easy, by allowing us to enter our startup script right in the configuration of the VM.  

Navigate back to your VM instances list and click on your VM name and then click edit. Scroll down and look for ‘Custom Metadata’. In the left hand box type ‘startup-script’. In the right hand box, type your script directly. Below is the script I used. The first line says that this is a shell script. The second line says to run my python script (be sure to write the full directory to the script. You can check the name of your working directory in SSH by typing ‘pwd’). The last line says to shut down the VM instance. Save your changes to the VM.  

    #! /bin/bash

    python3 /home/directory_name/mypythonscript.py

    shutdown -h now

Now if you were to shut down your instance and start it up, your script should automatically run and then your instance would shut itself down and you would see results in your BigQuery table. **WRONG!** Unfortunately you will get some error if you do this. To check your startup script output:  

    sudo journalctl -u google-startup-scripts.service

This is because the startup script is not executed from your home path; it’s executed at the root directory. Which means that your installation of your python modules from the home directory, although it’s nice if you want to play around with your script and run things quickly while in SSH, those installations are not accessible at root. So you will need to install them at the root directory. Do this by navigating to the root, and installing the requirements.txt file.  

    sudo su root

    sudo pip install -r /home/directory_name/requirements.txt
    
Now this should do the trick. When you start your instance back up, it should run successfully, and data should populate your table.  


**Scheduling Your VM Instance to Start**  
To round this whole thing off, we just need to schedule our VM instance to start automatically (we already have the stop part covered in the startup script). This involves adding a label to your instance that will correspond to a schedule you will create, as well as a cloud function you’ll create for the purpose of starting the VM. Google has great documentation on how to do this step by step, which you can find [here][start-stop-compute-engine].  

You now have hosted a python script on a google virtual machine, which you have scheduled to start up at a certain cadence, run your script, and shut down the machine. That wasn’t so bad.  


[start-stop-compute-engine]: https://cloud.google.com/scheduler/docs/start-and-stop-compute-engine-instances-on-a-schedule 