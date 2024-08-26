# AWS_VPC_and_EC2

As a part of my AWS re/Start training, I had to build a virtual private cloud (VPC) and other network components required to deploy resources, such as an Amazon Elastic Compute Cloud (Amazon EC2) instance.

## Create the VPC

Firstly, I log in the AWS Management Console and go to the VPC console. There I choose the option Create VPC.

![Screenshot (97)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/d7993582-973b-4aa7-abaa-e37bbd004629)

I configure the name and the IPv4 CIDR and choose Create VPC.

![Screenshot (98)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/0350a959-8ec3-4ae7-b545-3ecc3e86fe44)

Then I choose Edit VPC settings and in the DNS settings section, I select Enable DNS hostnames.

![Screenshot (99)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/e6ea46fa-3e27-487c-ace6-0dbc64e6eddb)
![Screenshot (100)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/14095ae1-a981-4372-bb04-54fd9032e249)


## Create Subnets

After that I proceed to create a public and a private subnet.

![Screenshot (101)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/8bf52d44-19e3-4c3c-9ea1-adc5d539063e)
![Screenshot (102)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/8b06b935-e707-4cd2-870d-35e8dabcf3f2)
![Screenshot (103)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/d5fd5957-6536-447a-a0e0-3366d7cb6d0a)
![Screenshot (104)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/665b2b16-372d-4248-9ea9-e9c81adb6c0c)
![Screenshot (105)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/26a81061-d7e2-428b-8fdd-d7c992841430)

## Create Internet Gateway

Then, I proceed to create an Internet Gateway in order to establish outside connectivity to EC2 instances in VPCs. After I create it, I attach it to my VPC.

![Screenshot (106)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/1fc6e9dc-849f-42fd-aa69-12b148a1feba)
![Screenshot (107)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/e22f1a22-482d-4398-abd5-4a93eb06ada0)
![Screenshot (108)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/3667a70d-0cef-4c89-81dc-087210f1174b)

## Configure route tables

After that, I configure the route tables. In the route tables list there is already one attached to my VPC. I edit its name to Private Route Table.

![Screenshot (109)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/5929428c-06d8-41da-9781-b74a68df61f6)

And after doing so, I create a Public Route Table.

![Screenshot (110)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/54ad0d9d-0f19-4a6a-9ee0-19621ae096cd)


In the Public Route Table, I add a route to the Internet Gateway I created earlier and I associate it with the Public Subnet.

![Screenshot (111)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/618ed7b5-9e26-41b8-a644-529b20df78c2)


## Create a bastion server in the public subnet

Moreover, I launch an EC2 instance bastion server in the public subnet that I created earlier.

![Screenshot (113)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/ba117a1a-ff38-400d-8c0a-5404ff8c04b3)
![Screenshot (114)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/290bf657-62a3-43f6-80cc-0914cde50000)
![Screenshot (115)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/efeccaf1-785a-4445-9b37-c5cb6d443429)

## Create a NAT Gateway

In addition, I launch a NAT gateway in the public subnet and configure the private route table to facilitate communication between resources in the private subnet and the internet. 

![Screenshot (116)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/cd0420a6-a9f4-4078-abd4-13af173f8db5)
![Screenshot (117)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/8a337f6a-2b33-431a-94a4-0535efdb0080)

## Create a private instance

Moving next, I launch an EC2 instance in the private subnet.

![Screenshot (118)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/6a24d16e-833a-45e8-9f5e-0b4e2176f721)
![Screenshot (119)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/86cbeacb-11b9-4eb5-bb85-a484d4c6a290)
![Screenshot (120)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/6b6093da-0715-4d1e-a807-9c8dc5b00328)

In the user data section, I enter a script which, for lab purposes, permits login by using a password.

![Screenshot (121)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/63280320-88b6-47b9-88fe-472e249fdfc2)

My instances are ready.

![Screenshot (122)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/58a336c7-fb32-4cee-acc8-772a0a1b17ca)

## Logging in to the bastion server and the private instance

It is not possible to directly log in to the Private Instance. Instead, I need to first log in to the bastion server in the public subnet and then log in to the private instance from the bastion server. In this caes, I am using EC2 Instance Connect to connect to the Bastion Server.

![Screenshot (123)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/6d714fb8-39d5-4c75-ac69-67ea03d978df)

Then I log in to the Private Instance.

![Screenshot (124)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/46aa4606-8b16-42de-a4da-ea03cecb2c87)
![Screenshot (125)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/13d15495-ef97-4438-b032-25395bf77c33)

## Test the NAT Gateway

The final part of this lab is to test the NAT Gateway I configured earlier. For this purpose, I am going to run the ping command.

![Screenshot (126)](https://github.com/DespoinaTikt/AWS_VPC_Configuration/assets/166096217/bbaabca3-65bc-4df6-b8ba-f3d4411bfc50)

The output indicates that the Private Instance successfully communicated with amazon.com on the internet, and my network configuration is successful.






