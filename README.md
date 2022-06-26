[version_1.0]

©2021 Amazon Web Services, Inc. and its affiliates. All rights reserved. This work may not be reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited.

Errors or corrections? Contact us at https://support.aws.amazon.com/#/contacts/aws-training.

Building a Simple AWS CloudTrail Data Analytics Solution
Before starting
The next video demonstrates the steps that are listed here, This document includes the step-by-step instructions that Raf completes on the Part 1 of the demo you are about to watch. You can use this document as a reference guide, or follow up in your own AWS account, which might incur some costs and is not mandatory for completing the course.

Important: If you choose to use your own account, make sure that you shut down the AWS resources you created after you finish using them, but only do so after finishing part 3.

The demo will show how you can visualize AWS CloudTrail data in Amazon QuickSight and start building simple security dashboards. Although CloudTrail is enabled by default in every AWS Account, Raf will configure a new trail, and also to show where CloudTrail configurations are made.

After configuring a new trail, Raf will add a new user into his AWS account (named nicholas). He will then log in as that user and do some activity that simulates a user who is issuing application programming interface (API) calls. One of these API calls will (accidentally) turn off a web server. If you want to follow the exact instructions in your account, you can mimic the scenario that Raf has in his account before you enable CloudTrail. To do so, you can create an Amazon Elastic Compute Cloud (Amazon EC2) instance to function as the web server.

After Raf turns off the web server as the user nicholas, he will log out and log in again as an administrator. Raf will then he will use CloudTrail data to investigate what happened by getting information, such as when the server was turned off. He will also discover the other API calls that the nicholas user made, because that account could have been compromised.

If you prefer decide to follow the instructions in your own account, make sure that all your resources are created in the N. Virginia AWS Region. The AWS Region can be located on the upper-right area of the AWS Management Console.



Part 1: Configuring CloudTrail and adding a secondary IAM User
As an AWS administrator: In the AWS Management Console, open the list of all AWS services by choosing Services, and then locate and choose CloudTrail.

Choose Create trail.

For Trail name, enter default. If that Trail name already exists in your account, enter: default_analytics

In the Trail log bucket and folder box, keep the default name suggestion. Note that this S3 bucket is the bucket where CloudTrail will store information. Make sure that you copy this bucket name because you will need it when you create the Amazon Athena table in Part 2.

Clear the Log file SSE-KMS encryption check box.

Scroll to the bottom of the page and choose Next.

On the next page, select Management events, Data events, and Insights events.

Scroll down to the bottom of the page and choose Next.

Review the information and choose Create trail.

You now have a new CloudTrail dataset that is being created in the designated bucket. You can go to Amazon S3 and inspect how the data structure will look like, as Raf did. As you interact with the AWS Management Console, your user is issuing API calls, which are captured and stored by CloudTrail.

As an AWS administrator: In the AWS Management Console, open the list of all AWS services by choosing Services, and locate and choose IAM.

In the navigation pane, choose Users and then choose Add user.

For the User name field, enter: nicholas (all lowercase).

For Access type, clear Programmatic access and select AWS Management Console access.

For Console password, choose Custom password and enter a password for the nicholas user.

Clear the User must create a new password at next sign-in check box and choose Next: Permissions.

On the Set permissions page, choose Attach existing policies directly.

In the Filter policies box, search for and select AmazonEC2FullAccess and AmazonS3FullAccess.

Choose Next: Tags, then choose Next: Review, and then choose Create user.

In the Success page, copy the displayed IAM sign-in URL, and then choose Close. If you inadvertently didn’t copy the URL, you can also locate it on the main IAM page by opening the IAM dashboard, as in the following screen capture:



Now you have a secondary IAM user (nicholas) that has the permissions to fully interact with Amazon EC2 and Amazon S3. Log out and log in as the new nicholas user by using the sign-in URL.

You can verify if you are logged in with the nicholas user by looking in the upper-right are of the AWS Management Console:



In the nicholas account, issue some API calls by navigating through the AWS Management Console. All your actions will be captured by CloudTrail.

While you are logged in to the console as nicholas, shut down an EC2 instance. Before you shut down any EC2 instances, make sure that you don’t need them, or that you created an additional EC2 instance specifically for this exercise.

Log out as nicholas and log back in as the administrator because you will next use Amazon Athena to query CloudTrail data!

