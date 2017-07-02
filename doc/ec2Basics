
## In this chapter we would:
# Learn about Amazon EC2
# Install a linux machine(a.k.a instance) on AWS EC2
# Create an EC2 ssh key pair
# Open a ssh port on the AWS instance that we have created
# Then access the installed instance via ssh using secure key pair

# EC2 stands for Elastic Compute Cloud. This service allows you to install and configure your desired operating system on a Virtual Machine, also known as instances. It mainly consists of the following components.
Instances: Virtual machines 
# Volumes: Data volumes, similar to hard disk of our Desktop or Laptops
# Key pairs: 'ssh' key used to access the instance remotely
# Load Balancer: Elastic Load Balancing automatically distributes incoming traffic across multiple EC2 instances. You create a load balancer and register instances with the load balancer
# Security Group: Security group is virtual firewall that controls the traffic for one or more instances. When you launch an instance, you associate one or more security groups with the instance. You add rules to each security group that allow traffic to or from its associated instances
# Elastic IP: An Elastic IP address is a static IP address that you can assign to your instance. This indicates that there are other type of IP addresses which are not static and keep changing.

Before proceeding please go through the following AWS videos which would help you to understand the features and know how they can be accessed via the GUI popularly called as Management Console

To access the videos please go to the url
https://aws.amazon.com/training/intro_series/

and then watch the following three videos 
- Introduction to Amazon Elastic Compute Cloud (EC2) 
- Introduction to Elastic Load Balancing 
- Introduction to AWS CloudFormation

By now you have fair idea about how instances can be created via the console. Now we would try to  
install the AWS instance using Cloud formation template and access it via ssh on port 22. 

## Steps to implement the above.
- Sign in to your AWS Console at https://aws.amazon.com/console/

## Steps to Create a Key Pair.
- From Console Click on EC2 on top right corner
- Click on Key Pair
- Click the button Create Key pair
- Enter key pair name in the text box and click on Create button
- The key would be created and automatically downloaded to your machine
- Save and remember it, without it you cannot access the AWS instance that you would create

### Steps to create an instance using cloud formation template
Cloud formation template follows a simple json structure as described below

{
 	“AWSTemplateFormatVersion” : “2010-09-09”,
			“Description” : “A Demo Application”,
                                    	“Parameters” : {
                                     		“<ParameterName>” : {
   					“Type”: “<Parameter type as defined by AWS>”
                                                	}  
                                   	},
			“Resources” : {
                                    		“<Resource Ref defined by user>” : {
					“Type” : “<Resource type defined by AWS>”,
					“Properties” : {
						<AWS defined property>:<property values>,
						<AWS defined property>:<property values>
					}
				}
			}
		}

## Describing various fields of the Cloud Formation Template.
- AWSTemplateFormatVersion: Specifies the version of the template format that user have provided
- Parameters: Place holder to define variables which would take it's value from the user when the template is given to 
AWS to create the resources. For us it would be the AWS key pair. There can be multiple parameter in this section.
- Resources: Place holder to define the resources that you are requesting to AWS. For us in this case it would be an AWS EC2 instance. There can be multiple resources in this section.

From the above description it appears that we have to know the format for the following
Key pair within parameter, which is
"KeyPairName": {
			“Description” : “Key Pair”,
			“Type” : “AWS::EC2::KeyPair::KeyName”,
			“ConstraintDescription” : “must be the name of an existing EC2 KeyPair.”
		}
Instance within resources, which is
		“EC2Instance” : {
			“Type” : "AWS::EC2::Instance",
			“Properties” : {
				“InstanceType” : “t2.micro”,
				“KeyName” : { “Ref” : “KeyPairName” },
				“ImageId” : “ami-bff32ccc”
			}
		}
	
	Value of instanceType which in this case is 't2.micro' can be selected from here	https://aws.amazon.com/ec2/instance-types/

	This tutorial uses Amazon Linux Image, so the value of ImageId can be found at 	http://aws.amazon.com/amazon-linux-ami/
 
	Generally you create your own OS Image or you buy one from amazon market place 
	https://aws.amazon.com/marketplace check Operating System on left hand side
	
	Pay attention to KeyPair highlighted in yellow. This parameter is defined in the Parameter 	section and later referred in Resources section using Ref. In AWS cloud formation any 	property can either take it's value directly like we have seen for  instanceType and  ImageId 	OR can refer to parameter like we have seen for KeyName.

	You can see the template https://github.com/pawansharma15/awsLearn/blob/master/intro_demo1
	Save this as text file in you local machine as it would be needed while creating the stacks.


## Steps to submit the AWS Cloud Formation template to AWS via the Console
- Login to AWS console
- Under Management Tools click on CloudFormation 
- Click on button Create New Stack
- Select the radio button Upload a template to Amazon S3
- Browse and select the template file you have saved
- Click on Next
- Give a name to the stack
- Choose the KeyPairName from the dropdown. Remember AWS is asking for user input because you have specified in the template that the value to parameter KeyPairName would be taken from the user. Select the key that you have created in the beginning. Click on Next
- Leave Tags and other options to default settings in the next page and click on Next
- Review and click on Create
- You can see the progress of the stack creation on the Events tab, selected by default
- Once the status reaches CREATE_COMPLETE
- Click on Ouputs tab and copy the value of InstanceId
- Go to Console Home Page(Click on top most right AWS icon)
- Click on EC2
- Click on Running Instance
- Paste the value of InstanceId copied in step 13, in the text box and hit Enter
- Select the instance 
- Note down the value of Public IP

Till here we have created an AWS instance and noted it's Public IP address. 

## But how to access it?
You would need the ssh key that you have saved in the beginning of the exercises. If you are using linux/unix machine then you type the following to get ssh access to the instance.
ssh -i <Key_File> ec2-user@<Public IP>
If you are on Windows then please use Putty with the cert to get ssh access to those instances.

## Opssss!!!
If you are here and you cannot access those instances using putty or by the above ssh command, then my apologies. We have created the instance but we have not opened the port 22. So, although AWS has created the instance for us and we would be billed for it. But we would not be able to use/access it as we have not opened any ports. 

## How to open a port?
As mentioned in the beginning that Security group is virtual firewall, which is mainly used to open ports in an instance. By default an instance can communicate to the whole world but no one from outside can access the instance unless we request AWS to open some ports on the instance using Security group. Now we have to open port 22 on the instance using the security group. Below is the Cloud Formation Template for security group, this template should go inside the Resources section of the template. 

"<SecurityGroupNameDefinedByUser>" : {
	"Type" : "AWS::EC2::SecurityGroup",
	"Properties" : {
		"GroupDescription" : "Security groups",
		{
			"SecurityGroupIngress" : [
				{
					"IpProtocol" : "tcp",
					"FromPort" : "22",
					"ToPort" : "22",
					"CidrIp" : "0.0.0.0/0"
				}
			]
		}
	}
}


CidrIp: It defines what IP address range can access your instance.  0.0.0.0/0 means everyone.

For details about security group please refer to http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-security-group.html

Once you put the above security group definition in your template which should look like https://github.com/sharmp07/demo/blob/master/demoTemplateSecurityGroups_demo2 and create a stack again BUT with a different name. Following the steps described in the section 'Now we have the template, what's next?' you would be able to gain ssh access to it.

Remember you have to associate the security group with the instance by adding this line to the instance definition in the resources section. 
"SecurityGroups" : [ { "Ref" : "<SecurityGroupNameDefinedByUser>" } ],
Please check the resource 'InstanceSecurityGroup' and the way it has been accessed inside the instance. 

## Please Delete the stack before proceeding to the next chapter by following the steps below
- Click on this icon on the left corner 
- Click on CloudFormation
- Select your stack
- Click on Action button and select Delete option
- Wait until the delete is complete

