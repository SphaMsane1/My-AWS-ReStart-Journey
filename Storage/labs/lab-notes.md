# AWS S3 Challenge Lab

## Lab overview

In this challenge, I worked with Amazon S3 to practice creating and managing storage resources. The goal was to create an S3 bucket, upload a file, configure permissions, and test access through a browser and the AWS CLI

## Objectives

By the end of this exercise, I was able to:

- Create an S3 bucket

- Upload an object into the bucket

- Make the object publicly accessible

- Access the object through a web browser

- List the contents of the bucket using the AWS CLI

## Steps I Followed

1. ### Connecting to the CLI Host

I started by connecting to the CLI Host EC2 instance using EC2 Instance Connect. This gave me a Linux terminal where I could run AWS CLI commands.

2. ### Configuring the AWS CLI

I set up the CLI with the credentials provided in the lab:

aws configure

- Access Key ID → (from lab details)

- Secret Access Key → (from lab details)

- Default region → us-west-2

- Output format → json

3. ### Creating and Working with S3

#### Create a bucket:

aws s3 mb s3://sphamandla-buc

#### Upload a file:

aws s3 cp "C:\Users\spha\OneDrive\Desktop\index.html\" s3://sphamandla-buc/

#### Make the object public:

aws s3api put-bucket-policy \
  --bucket sphamandla-buc \
  --policy '{
    "Version": "2012-10-17",
    "Statement": [
      {
        "Sid": "PublicReadGetObject",
        "Effect": "Allow",
        "Principal": "*",
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::sphamandla-buc/*"
      }
    ]
  }'

#### Test in browser:

http://sphamandla-buc.s3.amazonaws.com/index.html

#### List bucket contents:

aws s3 ls s3://sphamandla-buc

## Results

- I was able to see my uploaded file in the browser after making it public.

- Listing the bucket with the CLI confirmed the file was stored correctly.

## Key Takeaways

- Bucket names must be globally unique.

- It’s best practice to make objects public instead of entire buckets.

- AWS CLI makes it quick to manage and verify S3 operations.

## Conclusion: 

I successfully created an S3 bucket, uploaded and shared an object, tested it through a browser, and listed contents using the AWS CLI.
