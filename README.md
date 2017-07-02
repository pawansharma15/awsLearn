# awsLearn
Learn AWS Cloud formation template

The project contains series of steps for requesting resources using Cloud Formation Template, begining with creation of IAM user. This contains instructions to create accounts to be used by users while doing the hands on. I have created a Cloud formation template which would create 10 users at a time given. All the users would have the same password. The template creates uses in multiple of 10, so even if you want 11 users you have to create 10 users twice, which is 20 users.

- [Introduction - Create Users](https://github.com/pawansharma15/awsLearn/blob/master/create-users): This is a beginners template to create multiple IAM users
- [Template To Create An Instance](https://github.com/pawansharma15/awsLearn/blob/master/intro_demo1): Template to create an instance. Note this instances would not be accessile as there are no open ports for SSH.
- [Instance with Security Groups](https://github.com/pawansharma15/awsLearn/blob/master/demoTemplateSecurityGroups_demo2): Template to create an Instance along with open port using security group
- [Host a small node app in the Instance](https://github.com/pawansharma15/awsLearn/blob/master/autoStartHelloWorld_demo3): Use Cloud Formation template to create an instance, open port and host a "Hello World" node app
- [Elastic Load Balancer for two 'Hello World' instances](https://github.com/pawansharma15/awsLearn/blob/master/helloWorldLoadBalancer_demo4): In this example two "Hello World" apps would get balanced load from an ELB
