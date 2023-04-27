# Boto3-Python-SDK
Here is the code of Boto3 SDK for AWS services like EC2, IAM, S3, DynamoDB and other services

# What is Boto3 ?
* Boto3 is the Amazon Web Services (AWS) Software Development Kit (SDK) for Python.
* Boto3 is maintained and published by Amazon Web Services.
* Boto3 allows us to directly create, update, and delete AWS services from our Python scripts.

<a href="https://boto3.amazonaws.com/v1/documentation/api/1.14.0/index.html">Boto3 Documantation</a

## Installation:
Install the latest Boto3 release via pip:
```pip3 install boto3```

Configure root/IAM user:
```aws configure --profile <profile-name>```

provide access key and Secret access key:
```(Get it from IAM user-->Security Credentials)```
##### Access key & Secret access keys are stored in .aws/credentials

## IAM Section:
### Steps to see/list iam users:

1. Get AWS management console
2. Get IAM console
    options: Users, Groups, role,..


```js
//create iam.py file  --> vi iam.py

import boto3
aws_man_con=boto3.session.Session(profile_name="default")  //getting aws management console
iam_con=aws_man_con.resource('iam') //getting service console ('s3'),('ec2'),('iam'),etc

for each_user in iam_con.users.all():    //options: users/groups/role
	print(each_user.name)                //printing all users

//run iam.py file --> python iam.py 

```

## EC2 Section:
### Start the EC2 Instance

```js
import boto3
 
ec2 = boto3.client('ec2','ap-south-1')
 
response = ec2.start_instances(InstanceIds=['i-0fd7f6ee4e65c82a3'])
print(response)
```

### Run the EC2 Instance

```js
import boto3
 
ec2 = boto3.client('ec2','ap-south-1')
 
response = ec2.run_instances(ImageId='ami-0cca134ec43cf708f',InstanceType='t2.micro',KeyName='amar-key-pair',MinCount=1,MaxCount=1)
print(response)

```

## S3 Section:
### Create s3 Bucket:
```js

import boto3
 
s3 = boto3.client('s3')
 
response = s3.create_bucket(Bucket='mybucket-vaibhav',CreateBucketConfiguration={'LocationConstraint': 'ap-south-1'})
print(response)

```

### List S3 buckets:

```js

import boto3
 
s3 = boto3.client('s3')
 
response = s3.list_buckets()
arrlen = len(response['Buckets'])
 
for i in range(0,arrlen):
    print(response['Buckets'][i]['Name'])

```

### List S3 object:

```js
import boto3
 
s3 = boto3.client('s3')
 
response = s3.list_objects(Bucket='my-s2-vaibhav')
 
arrlen = len(response['Contents'])
 
for i in range(0,arrlen):
    print(response['Contents'][i]['Key'])

```

### Download the file from S3 Bucket:

```js
import boto3
 
s3 = boto3.client('s3')
 
response = s3.download_file('my-s2-vaibhav','boto.py','sample.py')
print(response)

````

### Delete object from S3 Bucket:

```js
import boto3
 
s3 = boto3.client('s3')
 
response = s3.delete_object(Bucket='my-s2-vaibhav',Key='boto.py')
print(response)

```

### Delete Multiple objects from S3 Bucket:

```js
import boto3
 
s3 = boto3.client('s3')
 
response = s3.delete_objects(Bucket='my-s2-vaibhav',Delete={
        'Objects': [
            {
                'Key': 't1.txt',
            },
            {
                'Key': 't2.txt',
            },
            {
                'Key': 't3.txt',
            },
            {
                'Key': 't4.txt',
            },
        ],
    })
print(response)

```
