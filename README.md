# Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI

Scenario: Level Up Bank is always looking for ways to improve it’s infrastructure and security. In this project, we were tasked with creating a new Apache website using Amazon Linux. This time around, Level Up bank wants us to create a user-data script that can be used when launching EC2’s to help expedite Linux package installations as well as Installing Apache. This would help them save time if there’s ever the need to rapidly scale the website.

Project Overview: This project has 3 tiers of difficulty. Foundational, Advanced and Complex. I will be challenging myself to complete all 3 tiers and will be breaking down each tier’s tasks and steps.

# Tier 1: Foundational

The tasks for this tier are:

— Create a t2.micro EC2 instance with the OS of your choice (Just make sure it is free tier).
— In the user-data field, use a script that updates all packages, installs Apache, and starts the Apache service.
— Verify that the instance has the Apache webserver downloaded and installed through the public IP.

Let’s get started!!!

The first thing we need to do is head over to the EC2 console and and click on Launch instance. Give the instance a name. I will be choosing Amazon Linux for the OS. Create a key pair and create a new security group allowing HTTP traffic from the internet.

![Snipe 1](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/07e2011c-abed-4385-8071-045d1b2fd67a)

![Snipe 2](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/f2fee4a1-eaf2-4b1a-a4a5-cb342de2440f)

Before we launch the instance, we have to add the user data. Scroll down to Advanced details section and expand it. You will have to scroll down once more until you reach User data -optional. Here is where we will paste the script that will update all packages and install Apache for us.

![Snipe 3](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/0d963cf4-660f-45a5-b598-efc6d8e94545)

Now click on Launch instance. After the instance is done provisioning, we will have to log into it and verify that all packages and Apache were installed.

We can check for updates by running sudo yum update

![Snipe 4](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/ba90e199-e361-49df-96fa-ff19bea2043c)

Looks like all updates were installed. Now to check on Apache. The following command will check Apache’s status: systemctl status httpd

![Snipe 5](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/84109b1c-9d1d-4d82-85ee-ebf92a967706)

The user data script worked perfectly. All updates were installed, Apache was installed, started and enabled.

Now to retrieve the public IP to see if we can reach it via browser.

![Snipe 6](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/3db47515-4761-4d20-9c9b-bec4d7a4be8c)

# Tier 2: Advanced

























