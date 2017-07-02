# Introduction
The document contains series of steps for requesting resources using Cloud Formation Template, begining with creation of IAM user. This contains instructions to create accounts to be used by users while doing the hands on. I have created a Cloud formation template which would create 10 users at a time given. All the users would have the same password. The template creates uses in multiple of 10, so even if you want 11 users you have to create 10 users twice, which is 20 users. The template to create the users can be found at https://github.com/pawansharma15/awsLearn/blob/master/create-users

## How to use the template to create users?
- First save the template in your computer as a text file
- Login to AWS console https://aws.amazon.com/console/
- Submit the Cloud Fromation template
- Please use a unique stack name, duplicate stacks name would result in error
- If you want more users repeat above steps, but with different stack name and get another list of 10 users and so on.

Now you have the users. These are IAM users, so they cannot login to the console directly but only as IAM users

## How the newly created IAM users can login to AWS Console?
- On your AWS console, not using the newly created users
- Click on the AWS icon on left top
- Click on link Identity & Access Management
- Copy the IAM user sign-in link and use the link for login

If you want to delete the users please delete the stacks.
