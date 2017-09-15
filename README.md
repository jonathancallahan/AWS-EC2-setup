# AWS-EC2-setup #

Makefiles to set up AWS EC2 instances with software to run Mazama Science data browsers.

The aim of AWS-EC2-setup is to make it easier to set up Mazama Science data browsers on a wide
variety of Unix variants. Different Makefiles exist for the different VMs offered by
[AWS](http://aws.amazon.com). Each Makefile is targeted to the needs of
[Mazama Science](http://mazamascience.com) for the installation of data browsers we build.

## Creating an AWS account ##

If you don't already have one, [create an AWS account](http://aws.amazon.com).

## Launching an Instance (notes from Zach Stednick) ##

1. Go to [aws.amazon.com](http://aws.amazon.com) and after logging in with your Amazon account (or
   creating a new Amazon account) click on the link for [EC2](https://aws.amazon.com/ec2/).
2. Click the button that says Launch Instance
3. AWS will walk you through a step by step process of setting up your
   EC2 instance. Step 1 of choosing an EC2 instance is choosing a machine instance.
   There are many server options with different OS types but I primarily use a 64-bit ubuntu server with the most recent release.
4. The next step is choosing an instance type. Generally I have found the bigger the instance the better and paying a few
dollars is generally better than using the free tier. I have never
needed to worry about connectivity so I usually go with something like
m4.xlarge
5. At this point in the step by step setup process the remaining steps are Configure Instance, Add
   Storage, Add Tags, Configure Security Group, and Review. I have never
had to use any of these features so I generally just click Review and Launch at this point.
6. AWS will bring up a confirmation screen and just click Launch.
7. AWS will ask if you want to use an existing public-key cryptography key pair or create a new key
   pair. In this case you will want to create a new key pair and then
download the <span style="background-color: #edeef0">`*.pem`</span> file you have just named and created.
8. AWS will now launch your instance - this takes a few minutes and you
   can observe the status at the EC2 dashboard (click on View Instances).

***
***

9. Once your instance is ready, you can log in with the following
   command <span style="background-color: #edeef0">`$ ssh -i <your EC2 pem file> ubuntu@<IPv4 Public IP>`</span>.
    - If you get an error about an unprotected private key file, change the permissions on your key file:
    <span style="background-color: #edeef0">`$ chmod 600 <your EC2 pem file>`</span> and it should work.
10. You should be sucessfully logged in at this point. Hooray!
11. At this point you will want to update your instance and install what
    ever software you want. Start by running <span style="background-color: #edeef0">`$ sudo apt-get update && sudo
    apt-get upgrade`</span>.
12. I got tired of trying to remember all the software libraries and dependencies I needed to install so I
    made a little setup shell script which I keep in my [dotfiles](https://github.com/stedy/dotfiles/blob/master/ec2_setup.sh).
13. You are now ready to work get to work on your EC2 instance. A few notes:
    - For file transfer you can use standard SFTP similarly to how you
      logged in: <span style="background-color: #edeef0">`$ sftp -i <your EC2 pem file> ubuntu@<IPv4 Public IP>`</span>.
    - Should you need to use [S3 file storage](https://aws.amazon.com/s3/) I would suggest using
      [s3cmd](https://github.com/s3tools/s3cmd), a command line utility for working with S3 objects.
14. When you are finished, go back to the dashboard and be sure to
    Terminate your session. Also best to delete your SSH keys as well.


***
