## Day_10: REACHABILITY ANALYZER

VPC Reachability Analyzer is a tool provided by AWS that helps us test and check if there are any problems with the connections between different resources in our virtual private clouds (VPCs).

Imagine you have set up multiple servers and services in your AWS account to run a big project. Sometimes, these resources may have trouble communicating with each other due to mistakes or errors in the way they are configured. It can be challenging and time-consuming to find out what's causing the issue.

VPC Reachability Analyzer comes to the rescue in such situations. It allows you to run tests and see if there are any connectivity problems between different parts of your project. By using this tool, you can quickly identify and fix any misconfigurations that may be causing network connectivity issues, making it easier to ensure that all your resources can talk to each other correctly.

For example, let's say you have a web server and a database server in your VPC. You want to make sure that the web server can connect to the database server. With VPC Reachability Analyzer, you can run a test to see if the web server can reach the database server and vice versa. If there's any problem or misconfiguration that is preventing them from talking to each other, the tool will help you identify and troubleshoot the issue.

In short, VPC Reachability Analyzer helps you troubleshoot and make sure that all the pieces of your project in the cloud can communicate with each other smoothly, saving you time and effort in resolving network issues.

**Below are the steps to practically perform a use case using the Reachability Analyzer to check the reachability between an EC2 instance and an Internet Gateway in your Virtual Private Cloud (VPC):**

1. Create a new VPC (Virtual Private Cloud).<br>
2. Give the VPC a name.<br>
3. Enter an IPv4 CIDR block (e.g., 10.0.0.0/16) for the VPC.<br>
4. Create the VPC.<br>
5. Create a subnet within the VPC.<br>
6. Click on "Subnets" in the VPC dashboard.
7. Select your VPC from the list.
8. Enter a subnet name, select an availability zone, and enter a CIDR block for the subnet (e.g., 10.0.1.0/24).
9. Click on "Create subnet."
10. Click on "Edit Subnet setting."
11. Click on "Enable auto-assign public IPv4 address."
12. Go to the "Internet Gateways" section.
13. Give the Internet Gateway a name.
14. Create the Internet Gateway.
15. After creating the Internet Gateway, a popup will appear saying "Attach to a VPC." Click on that popup and select your VPC to attach the Internet Gateway.
16. Create a route table for the VPC.
17. Click on "Route Tables."
18. Give the route table a name.
19. Select your VPC from the list.
20. Click on "Create route table."
21. Edit Subnet Association for the route table to include the subnet you created earlier.
22. Edit routes for the route table.
23. Click on "Add routes."
24. Select the Internet Gateway as the target.
25. Give the destination as "0.0.0.0" to allow traffic to all destinations (internet).
26. Create a Linux EC2 instance in your VPC and subnet.
27. Enable SSH port on the EC2 instance to allow remote access.
28. Go to AWS Network Manager (earlier reachability analyser comes in vpc).
29. Click on "Reachability Analyzer."
30. Click on "Create and analyze path."
31. Enter a name for the path analysis.
32. Select the source and destination for the connectivity test (e.g., EC2 instance as the source and Internet Gateway as the destination).
33. Select the source type as "Instances."
34. Choose the EC2 instance as the source.
35. Select the destination type as "Internet Gateway."
36. Choose the Internet Gateway ID as the destination.
37. Click on "Create and analyze path."
38. Now, in the Reachability Analyzer, you will see the entire path of the connectivity test.
39. Disconnect the connectivity by removing the Internet Gateway from the route table.
40. Check the Reachability Analyzer again and go to "Action" and "View details." You will find the test will run again and show an error, helping you identify where the issue is occurring and enabling you to rectify it.<br>

By following these steps, you can practically perform a use case of Reachability Analyzer to test and troubleshoot network connectivity between resources in your AWS Virtual Private Cloud (VPC).


## VPC - PEERING

A VPC peering connection is a networking connection between two VPCs that enables routing of traffic between them using private IP addresses. VPC peering connection can be established between our own VPCs, or with a VPC in another AWS account in a single or different region.

Think of VPC peering as a private connection between two virtual private clouds (VPCs) in AWS. It's like creating a direct, private pathway between two separate areas in a neighborhood. With VPC peering, these two VPCs can easily talk to each other using their own private addresses, just like neighbors talking across the pathway.

For example, imagine you have two VPCs in different regions. One is in New York, and the other is in California. Instead of sending messages or data through the internet, which can be slow and less secure, you create a private pathway (VPC peering connection) between the two VPCs. Now, they can communicate quickly and securely, making it easy for resources in one VPC to work with resources in the other VPC as if they were part of the same network

**In simple words:** VPC Peering allows us to connect two or more VPCs together so they can communicate securely.<br/>

To demonstrate the practical setup of VPC Peering, we'll create two VPCs: VPC1 and VPC2.<br/>

In VPC1, we'll create two subnets: a public subnet and a private subnet.<br/>

In VPC2, we'll create one private subnet.<br/>

Next, we'll create a peering connection between the public subnet and the private subnet in VPC1.<br/>

Finally, we'll establish a peering connection between VPC1 and VPC2, specifying the private subnets of both VPCs for communication.<br/>

Remember, it is important to enable the SSH port on both EC2 machines created within the private subnets of both VPCs. This step ensures they can securely establish a connection between each other.

**BENEFITS**

• Improve Security

• Save Money On Network Costs

• Get more flexibility for services that don’t need to connect to the Internet.

**LIMITATION**

• We cannot perform peering if both VPC have same CIDR, but we can perform VPC if you have a different CIDR.

• We cannot edit the VPC peering connection once it is created.

• We cannot attach or detach VPC peering connection

• Once we accepted VPC peering request we can’t change or deny it later


**Let's create VPC Perring**

1. Create First VPC

2. Name the VPC - VPC1

3. Give the CIDR - 10.0.0.0/16

4. Create VPC

5. Create Internet Gateway

6. Attach to VPC1

7. Create 2 Subnets

8. Select VPC1

9. Give name of subnet - Public-subnet-1

10. Give CIDR to public subnet - 10.0.1.0/24

11. Click on subnet. Click on Edit.

12. Click on auto assign public ip

13. Create 2nd subnet in VPC1

14. Give name of subnet - Private-subnet-1

10. Give CIDR to private subnet - 10.0.2.0/24

11. Create private subnet.

12. Create Route table

13. Give the name of route table. Attach VPC. Create it

14. Click on Action.

15. Edit subnet association

16. Assign public subnet.

17. Edit routes

18. Select target as Internet Gateway and destination as 0.0.0.0/0

19. Create EC2 machines

20. Create Linux EC2 Machines in Public Subnet

21. Create Security Group

22. Select type as SSH & Source as My IP

23. Click on Launch Instances

24. Create another EC2 in VPC1

25. Create Linux EC2 Machines in Private Subnet

26. Create Security Group

27. Select type as SSH & source as custom and give 10.0.1.0/24 means we are giving access to complete subnet so that whatever the EC2 machine are there in public subnet all can access to private subnet.

28. Launch the Instance

29. We have done setup for our first VPC

30. Create Second VPC

31. Name the VPC - VPC2

32. Give the CIDR - 28.200.0.0/16

33. Create VPC

34. Create subnet.

35. Give name of subnet - Private-subnet-2

36. Give CIDR to public subnet - 28.200.1.0/24

37. Create subnet.

**Note**- In second VPC we will not create internet gateway and route table because we don't need internet connection here.

38. Create EC2 machines

39. Create Linux EC2 Machines in Private Subnet

40. Create Security Group

41. Select type as SSH & source as custom and give 10.0.2.0/24 means we are giving access to complete subnet so that whatever the EC2 machine are there in private subnet VPC1 all can access to private subnet VPC2.

42. Also enable ping request to check connection between 2 VPCs<br/>
    Enable ICMP IPV4 and give 10.0.2.0/24 IP.

43. We have done setup for our second VPC

44. Connect Public-Subnet-1 of VPC1.

45. Now connect to Public-Subnet-1 of VPC1 to Private-Subnet-1 of VPC1<br/>
    To connect from public to private copy ssh command from Private EC2 instance and paste it in putty of public EC2 insatnce<br/>
    Previously we have seen that you will get an error because we need a PEM file.<br/>
    Earlier we were transfering PEM fuile with the help of winscp but we can also create it with the help of linux command.<br/>
    Everytime we cannot go with winscp because if we have to connect public intsnace to private instance we can go with winscp but if we have to connect private instance to another private instance this time we cannot go with winscp because there we need to provide public IP and we do not have public ip so we can go with linux commna dof creating PEM file.

46. Create pem file in the instance of Our Private Instance from first VPC - vim <pemfilename>.pem

47. In this PEM file we need to give some code. Open pem file in Notepad++

48. Copy the complete code & paste the code in putty

49. Change the permission of the file - chmod 400 <pemfilename>.pem

50. Switch user - sudo su

51. Connect Private Instance from first VPC<br/>
    paste SSH command of Private Instance

52. Now you will able to connect.

53. Now we need to connect from Private EC2 instance of VPC1 to Private EC2 instance of VPC2

**Note** - Here if we try to connect Private EC2 instance of VPC1 to Private EC2 instance of VPC2 with the help of PEM file then this will not work because here we don't have connection between VPC1 and VPC2.

54. We need to make the connectivity between two VPCs.

55. Create Peering Connections

56. Select Peering Connections

57. Click on Create Peering Connections

58. Enter the name

59. Select the Requester (First VPC)

60. Select my Account

61. same region

62. Select the Accepter (Second VPC)

63. Click on Create Peering Connections

64. This peering connection will not going to automatically setup. We need to accept the peering request.

65. Check if you able to connect Private EC2 instance of VPC2 with SSH command. <br/>
    No

66. We need to link the subnets means we need to craete routes in our both the subnets.

67. Create route table for first VPC

68. Go to route table. Create route table.

69. Give the name of route table.

70. Attach VPC1

71. Create route.

72. Click on Action. Edit subnet association.

73. Select private subnet.

74. Click on Action. Edit routes

75. Earlier we used to select "internet gateway" now this time we will select "peering connection". Give 28.200.0.0/16 IP address as destination because this time we are linking subnets with each other. We want to private subnet of VPC1 to private subnet of VPC2 so that is why in VPC1 we gave the ip of private subnet VPC2.

76. Same thing we have to do in VPC2

77. Create route of VPC2.

78. Click on Action. Edit subnet association.

79. Select private subnet.

80. Click on Action. Edit routes.

81. Give target as peering connection and destination as 10.0.2.0/16 (private subnet of VPC1)

82. Try to connect machine from private subnet of VPC1 to private subnet of VPC2 with the help of ssh command of private subnet of VPC2.

83. This time we will able to connect.

84. Also we can do ping request from private subnet of VPC1 to private subnet of VPC2 - ping 28.200.0.0/16, it will work.

85. **Can we do ping request from private subnet of VPC2 to private subnet of VPC1?**<br/>
      No, because in the private subnet of VPC2 we haven't enable ping request.<br/>

86. Go to Security group and enable ping request.<br/>
    Enable ICMP IPV4 and give 28.200.0.0/16 IP.

87. Now the ping request will work from VPC2 of private subnet.


## VPC - ENDPOINT

VPC endpoint is like a private tunnel that allows your resources (such as EC2 instances) within a Virtual Private Cloud (VPC) to directly and securely communicate with certain AWS services without needing a public IP address or going through the public internet.<br>

Here's an example to help you understand:<br>

Imagine you have a VPC on AWS, and you want your EC2 instances inside that VPC to access AWS services like Amazon S3 (cloud storage) or DynamoDB (NoSQL database) without exposing them to the public internet. With a VPC endpoint, you can set up a private connection between your VPC and the specific AWS service. This means your EC2 instances can securely access S3 or DynamoDB without needing public IP addresses, eliminating the need for an Internet Gateway, NAT Gateway, or VPN connection.<br>

In summary, VPC endpoints make it easier and more secure for your resources in the VPC to access AWS services privately, without the overhead and complexities of public internet access.

**ENDPOINTS - TYPES**

• Interface Endpoint

• Gateway Endpoint

**INTERFACE ENDPOINTS**:

Interface Endpoints are powered by AWS PrivateLink and provide private access to AWS services that are integrated with PrivateLink. These services have their own service-specific endpoint names, and they use Elastic Network Interfaces (ENIs) to establish connections between your VPC and the AWS service.

Interface Endpoints use private IP addresses, and the traffic stays within the AWS network, ensuring a secure and efficient communication channel.

Some AWS services that support Interface Endpoints through AWS PrivateLink include Amazon S3, Amazon DynamoDB, Amazon API Gateway, Amazon CloudWatch, and more.

**GATEWAY ENDPOINTS**:

Gateway Endpoints are used for accessing AWS services that support VPC endpoints but are not integrated with AWS PrivateLink. These endpoints use VPC route tables to route traffic directly to the service, making them easy to set up and manage.

Gateway Endpoints do not require ENIs, and they are associated with specific route tables in your VPC to direct traffic to the appropriate service.

As of now, Amazon S3 and Amazon DynamoDB support Gateway Endpoints for VPC access.

In this we will create 1 VPC<br/>
Under VPC we will create public subnet and private subnet
Then we will connect s3 bucket with private subnet with the help of VPC Endpoint.


**Let's create VPC Endpoint**

1. Create First VPC

2. Name the VPC - VPC

3. Give the CIDR - 10.0.0.0/16

4. Create VPC

5. Create 2 Subnets

6. Give name of subnet - Public-subnet-1

7. Give CIDR to public subnet - 10.0.1.0/24

8. Click on subnet. Click on Edit.

9. Click on auto assign public ip

10. Create 2nd subnet in VPC1

11. Give name of subnet - Private-subnet-1

12. Give CIDR to private subnet - 10.0.2.0/24

13. Create private subnet.

14. Create Internet Gateway

15. Attach to VPC

16. Create route table

17. Select VPC

18. Click on Action.

19. Edit subnet association

20. Assign public subnet.

21. Edit routes

22. Select target as Internet Gateway and destination as 0.0.0.0/0

23. In this we need two route tables. one we attach with public subnet and other we attach with private subnet.<br/>
    Also we have two route tables. One is just we created and earlier we have seen that whenever we creates VPC, AWS will create route table for use so that route table will use.

24. Attach the default route table with private subnet. For public subnet we have already created route table and attached to    public subnet.

25. Now Create End point

26. Go to Endpoint

27. Click on Create endpoint

28. Find S3

29. Select VPC

30. Select Private Subnet route table beacuse we are linking aws service with private subnet and then private subnet to public subnet.

31. Create Endpoint.

32. Create EC2 machines

33. Create Linux EC2 Machines in Public Subnet

34. Create Security Group

35. Select type as SSH & Source as Anywhere

36. Launch Instance.

37. Create another EC2 machines

33. Create Linux EC2 Machines in Private Subnet

34. Create Security Group

35. Select type as SSH & Source as 10.0.1.0/24(public subnet instances can access private subnet instances)

36. Launch Instance.

37. Now we are going to connect public machine and from public machine will connect private machine.

38. Connect Public machine of VPC.

39. Create Pem file to connect Private instance using Public Instance - vim <pemfilename>.pem

40. Change the Permissions - chmod 400 <pemfilename>.pem

41. switch user - sudo su

42. Copy & Paste the SSH Command of Private Instance

43. We will be connected to private subnet.

44. Earlier when we are using S3 service we are working with public subnet in case of NAT gateway. Now this time we are using private subnet.

45. switch user - sudo su

46. Connect to aws. Command to connect aws. Configure AWS - aws configure

47. Now generate access key ID and secrate key ID

48. Give the access key and secrate key ID

49. Enter Region - ap-south-1

50. Enter format - text

51. Create S3 Bucket - aws s3 mb s3://<Bucket_Name>

52. List of S3 Buckets - aws s3 ls

**Note** - Right now what we have created s3 we can create it from local machine, public machine so what is the purpose of endpoint and create s3 .<br/>
If we delete endpoint then we cannot create S3 and like in NAT gateway we don't need internet connection here.

**Endpoint is used whenever we want to connect aws service privately**    


## VPC - FLOW LOGS

VPC Flow Logs is a helpful tool that allows you to track and monitor the network traffic flowing in and out of your Virtual Private Cloud (VPC). It captures information about the IP traffic going to and from the network interfaces within your VPC.

Here's an example to make it clearer:<br>

Imagine you have set up a VPC on AWS, and it contains various resources like EC2 instances, databases, and load balancers. With VPC Flow Logs enabled, AWS will start recording details about each network packet that enters or leaves your VPC. This includes information like source and destination IP addresses, ports, protocols, and the amount of data transferred.<br>

Now, this data can be very valuable for troubleshooting network issues, analyzing security threats, and understanding the overall flow of traffic in your VPC. You have two options to store the captured flow log data:<br>

Amazon CloudWatch Logs: You can choose to publish the flow log data to Amazon CloudWatch Logs. This allows you to easily view and analyze the logs directly from the AWS Management Console or use CloudWatch features to set up alerts and perform real-time monitoring.<br>

Amazon S3: Alternatively, you can store the flow log data in Amazon S3, which is a highly scalable and durable object storage service. This option is useful if you want to retain the logs for an extended period or if you prefer to use custom analysis tools or third-party software to process the data.<br>

In summary, VPC Flow Logs provide essential insights into the network traffic within your VPC, and you can choose to store this information in either Amazon CloudWatch Logs or Amazon S3 for further analysis and monitoring.<br>


1. Create VPC

2. Name the VPC - VPC

3. Give the CIDR - 10.0.0.0/16

4. Create VPC

5. Create Subnet

6. Give name of subnet - Public-subnet

7. Give CIDR to public subnet - 10.0.1.0/24

8. Click on subnet. Click on Edit.

9. Click on auto assign public ip

10. Create Internet Gateway

11. Attach to VPC

12. Create route table

13. Select VPC

14. Click on Action.

15. Edit subnet association

16. Assign public subnet.

17. Edit routes

18. Select target as Internet Gateway and destination as 0.0.0.0/0

19. Create EC2 machines

20. Create Linux EC2 Machines in Public Subnet

21. Create Security Group

22. Select type as SSH & HTTP port and Source as Anywhere

23. Give the bootstarp script<br/>
    #!/bin/bash<br/>
    sudo su<br/>
    yum update<br/>
    yum install httpd<br/>
    cd /var/www/html<br/>
    echo "AmazonWebservices" > index.html<br/>
    service httpd start<br/>
    chkconfig httpd on<br/>

24. Launch Instance.

25. Check the public Ip of EC2 machine in the browser<br/>
    It will open.


**FLOW LOGS – S3**

1. Create S3 Bucket & Don’t give public Access

2. Go to S3.

3. create bucket

4. Giv the name of bucket.

5. Click on create bucket.

6. Now create flow logs in S3.

7. Go to VPC service. Select your VPC.

8. Below down we will find Flow logs section.

9. Create flow logs

10. Give the name of flow logs

11. Select filter <br/>
    Accept <br/>
    Reject <br/>
    All <br/>

12. Maximum Aggregation interval<br/>
    10 minutes<br/>
    1 minutes<br/>

13. Destination<br/>
    Send to an Amazon S3 Bucket

14. Give s3 bucket ARN<br/>
    To get s3 bucket ARN. Go to s3, select bucket you will get ARN. Copy ARN.

15. Select Log record format<br/>
    AWS default format<br/>
    Custom format

16. Click on create flow logs

17. Now go to s3, under bucket you will get logs


**FLOW LOGS – CLOUD WATCH**

1. Go to cloudwatch service

2. Go to log grups. Under this log group aws is creating logs

3. Give the name of log group

4. Select Retention days (After how many day aws log get expired)<br/>
   Select never expire

5. Create log group.

6. Now go to VPC

7. Click on flow logs

8. Click on create flow logs

9. Give the name of flow logs

10. Select filter as All

11. Select Maximum aggregation interval & Select Cloud Watch Logs

12. Give the destination log group which we have created in the starting of cloudwatch logs

13. To create this log group we need IAM role.<br/>
    Create IAM role<br/>
    Create policy<br/>
    select cloudwatch service<br/>
    Select actions <br/>
    In list Select (DescribeLogGroups, DescribeLogStreams)<br/>
    In Write Select (CreateLogGroup, CreateLogStream, PutLogEvents)<br/>
    Select resource as all resources<br/>
    Give policy name<br/>
    create policy<br/>

    Now create role<br/>
    Select custom trust policy<br/>
    We need to give seprate json code<br/>
    {<br/>
    "Version": "2012-10-17",<br/>
    "Statement": [<br/>
        {<br/>
            "Sid": "",<br/>
            "Effect": "Allow",<br/>
            "Principal": {<br/>
                "Service": "vpc-flow-logs.amazonaws.com"<br/>
            },<br/>
            "Action": "sts:AssumeRole"<br/>
        }<br/>
    ]<br/>
}<br/>
    Click on Next<br/>
    Select the policy which we have created<br/>
    Enter the role name & description<br/>
    Click on create role<br/>

14. Go back to VPC. select IAM role

15. Click on create Flow logs

16. Go to cloudwatch log group

17. Click on search log group

18. There we will find the logs


**Note**- In real time it is difficult to read those logs because there are 100s of lines logs.

To resolve ths issue we have Athena service. Wth the help of this we can read logs very easily by running few sql queries.It is showing in table format.We can link s3 bucket with this Athena service.


## S3 - ATHENA

Amazon Athena is a server less query service that makes analysis of data, using standard SQL, stored in Amazon S3 simpler. With few clicks in the AWS Management Console, customers can point Amazon Athena at their data stored in Amazon S3 and run queries using standard SQL to get results in seconds.

In Athena service we have to link s3 bucket.

1. Click on Edit Settings.

2. Browse our s3 bucket

3. Select the existing s3 bucket where we are storing VPC Flow Logs

4. Click on choose & Save

5. Go to Editor and start creating our tables.

6. So under particular dates whatever files we have sytem will going to read it.


## AWS - VPN CONFIGURATION (OPENVPN)

Amazon Web Services (AWS) offers Virtual Private Network (VPN) solutions to securely connect your on-premises network or data center to your AWS VPC (Virtual Private Cloud) over the internet. A VPN establishes an encrypted tunnel between your local network and the AWS cloud, enabling secure communication and data transfer between the two environments.

1. Check our Public IP<br/>
   Go to browser and type whatismyipaddress. We will get our Ip address

2. Create Open VPN EC2 Machine

3. Go to EC2 machine

4. Give name

5. There are predefine AMI we have in AWS<br/>
   click on Browse more AMI

6. We have AWS marketplace AMI. This is the third party AMI

7. Search OpenVPN

8. Click on select

9. Click on Continue

10. Select the Instance type as t2.micro

11. Use Default VPC & Subnet

12. System is creating the Security group.

13. Launch the instance

14. Note down EC2 machine public IP

15. Connect EC2 Machine with Putty

16. Earlier we are using username as ec2-user for linux type of instances but this time we are using openVPN and openVPN is of Ubuntu type of operating system.

17. So default username will be root.

18. It will install openVPN using root user.

19. Now it will ask you to login vpn

20. Again connect putty with user openvpnas

21. Now set openVPN password

22. Command to set password - sudo passwd openvpn

23. Enter our Password

24. Now try to connect your private network<br/>
    https://<publicip>:943/admin

25. Enter username (openvpn) & password

26. Click on sign in

27. Click on Agree

28. In openVPN we will enable one option

29. Click on VPN Settings

30. Go to Routing

31. Select yes for Internet traffic

32. Click on save setting

33. Now Login with user access<br/>
    https://<publicip>:943/

34. Enter our username (openvpn) & password

35. Download openvpn as per the operating system

36. Click on more info & then Click on Run anyway

37. Accept the terms & Install

38. Open tool openvpn

39. Click on Connect

40. Enter username & password

41. Check the IP Address from whatismyipaddress.com. You will find your system is connected with OpenVPN a private network.
    Your system Ip address has changed to openvpn ip address.
