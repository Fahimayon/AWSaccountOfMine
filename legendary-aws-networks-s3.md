<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Access S3 from a VPC

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-s3)

**Author:** MD. Fahim Parvez  
**Email:** parvez22205341185@diu.edu.bd

---

## Access S3 from a VPC

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-s3_3e1e79a2)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a logically isolated virtual network in AWS where you can launch and manage resources like EC2 instances, databases, and load balancers.

It is useful because it allows you to control networking, security, and connectivity for your resources, while still enabling secure access to AWS services outside the VPC, such as Amazon S3.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a secure, isolated network for my EC2 instance so that it could interact with AWS services outside the VPC, such as Amazon S3, demonstrating how resources inside a VPC can access and manage external AWS services securely.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how simple it is for an EC2 instance inside a VPC to securely access AWS services outside the VPC, like Amazon S3, once access keys are properly configured. It was surprising to see that the VPC’s isolation does not prevent communication with external AWS resources when permissions are set correctly.

### This project took me...

This project took me about 1.5 hours to complete 

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will set up a VPC and an EC2 instance because the EC2 instance is required to access S3 from within the VPC.

### Step 2 - Connect to my EC2 instance

In this step, I will connect directly to my EC2 instance because I need command-line access to interact with AWS services from inside my Amazon VPC, including testing access to Amazon S3.

### Step 3 - Set up access keys

In this step, I will create and configure access keys for my EC2 instance because the instance needs valid credentials to authenticate with my AWS account and securely access AWS services such as Amazon S3 through the AWS CLI.

---

## Architecture set up

I started my project by launching a VPC and an EC2 instance to enable secure access to S3.

I also set up sample files because they are needed to test S3 access from the EC2 instance.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-s3_4334d777)

---

## Running CLI commands

AWS CLI is a command-line tool that allows users to interact with and manage AWS services by running commands instead of using the AWS Management Console.

I have access to AWS CLI because it comes preinstalled on my EC2 instance, allowing me to run AWS commands directly from the server to access services like Amazon S3 using my AWS credentials.

The first command I ran was aws s3 ls. This command is used to list all the Amazon S3 buckets in an AWS account that the current credentials have permission to access, helping verify whether my EC2 instance can successfully communicate with Amazon S3 using the AWS CLI.

The second command I ran was aws configure. This command is used add AWS credentials so the CLI can access AWS services.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-s3_e7fa8776)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured the AWS CLI on the instance using the access key ID and secret access key, along with a default region and output format, because the EC2 instance needs permission to use AWS services.

Access keys are credentials that allow programs and servers to access AWS services securely.

Secret access keys are the private credential that, with an access key ID, lets a program securely access AWS services.

### Best practice

Although I’m using access keys in this project, a best practice alternative is to use an IAM role attached to the EC2 instance, which provides temporary credentials automatically and removes the need to store long-term access keys on the server when accessing services like Amazon S3.

---

## In the second part of my project...

### Step 4 - Set up an S3 bucket

In this step, I will create a new Amazon S3 bucket and upload two files into it because I need sample data to test and demonstrate how my EC2 instance inside the VPC can securely access and interact with S3 using the AWS CLI and the access keys I configured.

### Step 5 - Connecting to my S3 bucket

In this step, I will connect to my S3 bucket from the EC2 instance because I need to test secure access to external AWS services.

---

## Connecting to my S3 bucket

The first command I ran was aws s3 ls. This command is used to list all the Amazon S3 buckets in an AWS account that the current credentials have permission to access, helping verify whether my EC2 instance can successfully communicate with Amazon S3 using the AWS CLI.

When I ran the command aws s3 ls again, the terminal showed the S3 bucket I created. This indicates the EC2 instance is connected to the S3 bucket 

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-s3_4334d778)

---

## Connecting to my S3 bucket

Another CLI command I ran was aws s3 ls s3://nextwork-vpc-project-fahimayon, which returned the files I've uploaded into the S3 bucket 

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-s3_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command sudo touch /tmp/test.txt. This command creates a new, empty file named test.txt in the /tmp directory on my EC2 instance, which I can then upload to the S3 bucket as a sample object for testing.

The second command I ran was aws s3 cp /tmp/test.txt s3://nextwork-vpc-project-fahimayon. This command will copy the file test.txt from the EC2 instance’s /tmp directory to the specified S3 bucket, effectively uploading it as an object in the bucket so it can be stored, accessed, or shared from Amazon S3.

The third command I ran was aws s3 ls s3://nextwork-vpc-project-fahimayon, which validated that the file test.txt was successfully uploaded to the S3 bucket and confirmed that my EC2 instance could list and access objects in the bucket using the AWS CLI.

![Image](http://learn.nextwork.org/relieved_purple_wise_freshwater_mussel/uploads/aws-networks-s3_3e1e79a2)

---

---
