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

Now that we have an EC2 instance hosting our Apache web server, we need to create an AMI and spin up a new instance to test if we can reach it via browser just like we did in the previous tier.

Head back into the EC2 console and right click on the server. Then go to Image and templates then create image.

I am going to give it the same name as my original EC2 instance but will be adding Gold Image to it.

![Snipe 7](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/e2f230c2-7909-4dd4-a76b-8598a0e7024b)

Scroll down and click on Create image.

Just wait until the status changes to Available before continuing.

When it is Available, right click on the AMI and select Launch instance from AMI.

![Snipe 8](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/e5e4a780-686c-472c-bdc5-ec113c659fc3)

Give the new instance a name and make sure in the AMI from catalog section, that the proper AMI is selected. The next thing we need to do is select the same Key pair that we were using for the original instance, click on Select existing security group and choose the same one we created earlier. Then click on Launch instance.

![Snipe 9](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/010b063e-1636-4b2e-ae93-d374823aab92)

# Tier 3: Complex

— Perform all of the work in the previous 2 tiers via the AWS CLI.
Note: you can use a pre-existing AWS keypair and you are allowed to reference the AWS Console to get ID information.

I will be using PowerShell to do this step. After running AWS Configure, I ran the following command (screenshot below) to create the EC2 instance with user data.

*Note* (With each command that I will be using, I will be declaring my AWS profile due to having multiple AWS user accounts)

![Snipe 10](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/9d2eed77-34ae-469b-8edd-95b792fe80b6)

*Important* (For your user data to work, make sure you are in the directory where the text file is located)

Wait a couple of minutes to allow for the Linux packages and Apache to be installed. Now go to the EC2 console and copy the public IP address and paste it into a browser.

![Snipe 11](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/d94cb214-2a8f-42f7-891a-16b0d9dbac3a)

Now to make a copy of the AMI, we need to run the command below:

![Snipe 12](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/bc45f0e5-678f-4768-99e3-8f52a900cb06)

![Snipe 13](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/8179eefa-c2e9-468f-849c-44f1f6ff2e61)

Now that we have created the AMI image, we need to launch it then test for Apache connectivity via browser.

The following command launches an instance using the AMI copy (make sure you are using the AMI ID of the AMI image we just created):

![Snipe 14](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/791c5ebf-ee04-49bb-a1e7-0dddca9a1ea8)

After the instance is up and running, grab the public IP and paste it into a browser.

![Snipe 15](https://github.com/Mirahkeyz/Launching-An-EC2-Instance-With-Userdata-Via-AWS-CLI/assets/134533695/0e5d5f2f-3d33-4dea-a886-b66bdc87ea80)

























































