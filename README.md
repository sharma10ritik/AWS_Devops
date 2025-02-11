# Connecting Ec2 with S3 & hosting a page index.html

**Step 1: Upload index.html to S3**
Go to AWS Console → Open S3 service.
Create a Bucket (if not already created):
Click Create Bucket.
Name it my-project-1-2025.
Choose a region.
Disable Block all public access (if you want public access).
Click Create Bucket.
Upload the index.html file:
Open your bucket.
Click Upload → Select index.html → Click Upload.

**Step 2: Launch EC2 Instance**
Go to AWS EC2 Console → Click Launch Instance.
Choose an Amazon Machine Image (AMI):
Select Amazon Linux 2 or Ubuntu.
Choose Instance Type:
t2.micro (Free-tier eligible).
Attach IAM Role to EC2 for S3 Access:
In IAM Console, create a new IAM role with:
AWS Service → EC2
Policy: AmazonS3ReadOnlyAccess
Attach the role to your EC2 instance.
Configure Security Group:
Allow HTTP (port 80) for public access.
Allow SSH (port 22) for remote access.
Launch the Instance.

**Step 3: Install Web Server on EC2**
For Amazon Linux:
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd

**Step 4: Copy index.html from S3 to EC2**
Since I've attached the IAM role to your EC2 instance, you can now access S3 without configuring AWS credentials manually.

Check if EC2 can access S3:
>>  aws s3 ls s3://my-project-1-2025/

Download index.html to the Apache Web Directory:
>> sudo aws s3 cp s3://my-project-1-2025/index.html /var/www/html/index.html

Set Correct Permissions:
>> sudo Chmod -R 777 /var/www/html/

Restart the Web Server:
>> sudo systemctl restart httpd  # For Amazon Linux

**Step 5: Access the Website**

http://your-ec2-public-ip






