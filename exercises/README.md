# CloudFormation Exercises

These 'exercises'  are examples of things you can create using CloudFormation. They are in a rough order of difficulty but can be tackled in any order.

## 1. Website hosted on S3
Building upon the S3 demo (found at `demo/s3.yaml`) create a website hosted on S3. 

Hints to acheive this:
- The template should be updated so that the S3 bucket should allows access to the public and has the `'WebsiteConfiguration'` property set. 
- An index file for the homepage will need to be uploaded to the S3 bucket. An example index.html can be found at `exercises/index.html` 
- The index file itself will need to be have appropriate permissions set. 

## 2. EC2 access via SSH
Building upon the EC2 demo (found at `demo/ec2.yaml`, allow SSH access to the instance from your IP address only. 

Hints to achieve this:
- Find your IP address and convert to CIDR notation (for this case `${IP}/32` where `${IP}` is your IP address)
- Update `ec2.yaml` to allow add a rule for ingress SSH (port 22) access. 
- Create a KeyPair through the EC2 section of the AWS console and note the name.
- Update `ec2.yaml` to add the KeyName of your KeyPair to the ec2 resource.
- Authentication to this instance uses public key cryptography. The AWS documentation provides a good guide to help with how to connect to the instance [https://docs.aws.amazon.com/quickstarts/latest/vmlaunch/step-2-connect-to-instance.html#sshclient] 

Additional improvements:
- Use [CloudFormation parameters][cfn-parameters] to parameterise the KeyName and SSH IP location.

## 3. AutoScaling Group
Create an autoscaling group of instances that spans across two availability zones that has a maximum, minimum and desired number of instances of 1. Try terminating the instance and watching what happens.

To remain in the free tier you'll need to set the InstanceType property of the LaunchConfiguration resource to t2.micro

Hints to achieve this:
- You'll need three separate types of resources `AWS::AutoScaling::AutoScalingGroup` , `AWS::AutoScaling::LaunchConfiguration` and optionally a `AWS::EC2::SecurityGroup`
- The launch configuration and security group can be based upon the ec2 demo earlier.

Additional improvements:
- AMIs are a regional resource. Use Mappings to be able specify the ImageId of the AMI in different regions so you could use the template across different regions.

## 4. DynamoDB
Create a DynamoDB table to capture details of people attending the workshop.

## 5. AWS Lambda
Deploy the prebuilt lambda function `hello-lambda.zip` and test using the console.

Hint: You'll first need to upload the zipped package to S3
 
Hint: You will need to create an execution IAM role for your lambda function. If using CLI you'll need to set the --capabilities CAPABILITY_IAM option to acknowledge the creation of IAM resources

## 6. Other
Have you used any other AWS services previously?  Try provisioning them using CloudFormation. 

[cfn-parameters]: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html

