
We can skip Part 1 if we have a User and a Group already provisioned.<br>

Otherwise, make sure to create a User and a Group via `IAM`, https://console.aws.amazon.com/iam/home.

## Part 1 : create a User and a Group using IAM

- We log into our `AWS` management console using `$ https://console.aws.amazon.com.`<br>

I'm using `MFA` to secure my root account access coupled with `Google Authenticator` on my `Android` smartphone.<br>

We can bypass this step and login normally to `AWS` Management Console.<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-1.jpg](https://i.postimg.cc/L5F2KQwp/isaac-arnault-AWS-1.jpg)](https://postimg.cc/nj26q2nR)

</p>
</details>

We go to Services > IAM > Users > Add user<br>

<li>Your VPCs > Create </li><br>

<li>Access type : Programmatic access</li><br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-16.png](https://i.postimg.cc/Mpdv5JTN/isaac-arnault-AWS-16.png)](https://postimg.cc/fVSzWFYf)

</p>
</details>

<b> Next : Permissions > Create group</b><br>

<li>Group name : Developers</li><br>

<b>Administrator Access > Create group</b><br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-17.png](https://i.postimg.cc/cJC65ktH/isaac-arnault-AWS-17.png)](https://postimg.cc/Ty8RK99M)

</p>
</details>

<b>Next : Tags</b><br>

<li>Key: dev-1 | Value: name of the developer</li><br>

<b>Create user</b><br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-18.png](https://i.postimg.cc/sXpzn5mx/isaac-arnault-AWS-18.png)](https://postimg.cc/hzPNvzHR)

</p>
</details>

<b>Download .csv</b> (you're going to use these credentials later on in this tutorial)<br>

- We write down our Access key ID and Secret access key > close the window<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-28.png](https://i.postimg.cc/WzPg3281/isaac-arnault-AWS-28.png)](https://postimg.cc/FdD7CXwM)

</p>
</details>

- Now in Groups we should have one group named Developers which should list <b>user-1</b>.

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-20.png](https://i.postimg.cc/TPfZch1q/isaac-arnault-AWS-20.png)](https://postimg.cc/dhNHss8L)

</p>
</details>

<hr>

## Part 2 : create a custom Virtual Private Cloud - VPC - on AWS

- We log into our `AWS` management console using `$ https://console.aws.amazon.com.`<br>

I'm using `MFA` to secure my root account access coupled with `Google Authenticator` on my `Android` smartphone.<br>

We can bypass this step and login normally to `AWS` Management Console.<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-1.jpg](https://i.postimg.cc/L5F2KQwp/isaac-arnault-AWS-1.jpg)](https://postimg.cc/nj26q2nR)

</p>
</details>

We go to Services > VPC > Networking & Content Delivery > VPC<br>

Your VPCs > Create VPC > Name Tag: myVPC > IPv4 CIDR block : 10.0.0.0/16 (it's the biggest address block possible)<br>

Select : Amazon provided IPv6 CIDR block > Tenancy : Default > Create<br>

We go to "Your VPCs" to check if "myVPC" has been created.<br>

<details>
<summary>🔴 See output</summary>
<p>
  
[![isaac-arnault-AWS-50.png](https://i.postimg.cc/KzGwQbRQ/isaac-arnault-AWS-50.png)](https://postimg.cc/nsW3c6KQ)

</p>
</details>

Now let's create a `Subnet`. Go to "Subnets".<br>

<li>VPC : choose <b>myVPC</b></li><br>

<li>Name : myVPC - Subnet 1</li><br>

<li>AZ : choose <b>us-east-1a</b></li><br>
  
<li>IPv4 CIDR block : 10.0.1.0/24</li><br>  

<details>
<summary>🔴 See output</summary>
<p>
  
[![isaac-arnault-AWS-51.png](https://i.postimg.cc/bYbVbdC8/isaac-arnault-AWS-51.png)](https://postimg.cc/4nf1R4RF)

</p>
</details>

<details>
<summary>🔴 See output</summary>
<p>
  
[![isaac-arnault-AWS-52.png](https://i.postimg.cc/BnvChvgj/isaac-arnault-AWS-52.png)](https://postimg.cc/qz9nq4Wr)

</p>
</details>

Let's create another subnet<br>

<li>Name : myVPC - Subnet 2</li><br>

<li>AZ : choose <b>us-east-1b</b></li><br>
  
<li>IPv4 CIDR block : 10.0.2.0/24</b></li><br>
  
Let's check that the two subnets (Subnet 1 and Subnet 2) have been created : go to Subnets<br>

<details>
<summary>🔴 See output</summary>
<p>

[![isaac-arnault-AWS-53.png](https://i.postimg.cc/dV75s1Tz/isaac-arnault-AWS-53.png)](https://postimg.cc/CRgGJw7N)

</p>
</details>

We created two subnets to have a private and public subnet.<br>

Let's assign a public IP address to "myVPC - Subnet 1".<br>

Select "myVPC - Subnet 1" > Actions > Modify auto-assign IP settings > Check : Auto-assign IPv4 <br>

<details>
<summary>🔴 See output</summary>
<p>
  
[![isaac-arnault-AWS-54.png](https://i.postimg.cc/ry03jMjy/isaac-arnault-AWS-54.png)](https://postimg.cc/w3zwTKnn)

</p>

</details>

<details>
<summary>🔴 See output</summary>
<p>
  
[![isaac-arnault-AWS-54.png](https://i.postimg.cc/ry03jMjy/isaac-arnault-AWS-54.png)](https://postimg.cc/w3zwTKnn)

</p>

</details>

Let's add an `Internet Gateway` to our `VPC`.<br>

Click on "Internet Gateways" > Create Internet gateway > Name tag: myIG > Create<br>

We see that in our Internet Gateways dashboard, "myIG" State is "detached". Let's fix this.<br>

Select "myIG" gateway > click Actions > Attach to VPC (this will attach our IG to our VPC).<br>

Select "myVPC" > Attach.<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-55.png](https://i.postimg.cc/FFCcrQXS/isaac-arnault-AWS-55.png)](https://postimg.cc/t7P7kwTR)

</p>
</details>

Our IG is now attached to our VPC.<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-57.png](https://i.postimg.cc/1zKnbkKf/isaac-arnault-AWS-57.png)](https://postimg.cc/gwn2ZBQW)

</p>
</details>

<b>Important</b><br>
You can have only one IG per VPC.<br>

We now have to go to <b>Route Tables</b> to configure our main route.<br>

Click "Create route table" > Name tag: myPublicRoute > VPC: select myVPC > Create<br>

<details>
<summary>🔴 See output</summary>
<p> 

[![isaac-arnault-AWS-58.png](https://i.postimg.cc/y62mhzpH/isaac-arnault-AWS-58.png)](https://postimg.cc/14cVPbZC)

</p>
</details>

From "myPublicRoute", let's create a route out to the Internet.<br>

Select "myPublicRoute", select "Routes" > clic "Edit routes" > Add route > Destination : 0.0.0.0/0 > Target : select IGW ><br>

Add route > Destination: ::/0 > Target

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-60.png](https://i.postimg.cc/Jh7Z770b/isaac-arnault-AWS-60.png)](https://postimg.cc/68SyYXd3)

</p>
</details>

Select "Subnet associations" > Edit subnet associations > Select Subnet 1 to add it to your public route table > Save<br>

Let's check that "myPublicRoute" has a route out to the Internet. Select "myPublicRoute", click "Routes".<br>

<details>
<summary>🔴 See output</summary>
<p>
  
[![isaac-arnault-AWS-61.png](https://i.postimg.cc/sDRBDf0v/isaac-arnault-AWS-61.png)](https://postimg.cc/4nB4WGGg)

</p>
</details>

## Part 3 : create one EC2 instance in our Public Subnet and one in our Private subnet

Go to Services > EC2 > Launch Instance > let's create our 1st instance:  select Amazon Linux 2 AMI<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-62.png](https://i.postimg.cc/x8fWtz1X/isaac-arnault-AWS-62.png)](https://postimg.cc/cgz9J6YW)

</p>
</details>

Select t2.micro > Next: Configure instance Details > Network : change it to myVPC<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-63.png](https://i.postimg.cc/zvGcnYxW/isaac-arnault-AWS-63.png)](https://postimg.cc/62FcXgJ5)

</p>
</details>

Next: Add Storage (leave as default) > Next : Add tags > Add Tag > Key: Name > Value: WebServer-1<br>

Next: Configure Security Groups > Create a new security group > SG name : mySG > Description: My EC2 Security Group<br>

Add rule > Select HTTP > Review and Launch > Launch ><br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-64.png](https://i.postimg.cc/d3f4rkkP/isaac-arnault-AWS-64.png)](https://postimg.cc/fSxchbfB)

</p>
</details>

Create a new Key Pair > Name : KP > Download Key Pair > Launch instances > View instances <br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-AWS-65.png](https://i.postimg.cc/d096nSk9/isaac-arnault-AWS-65.png)](https://postimg.cc/bGs1wgRG)

</p>
</details>

Now let's create our second `EC2` instance.<br>

Launch instance > select Amazon Linux 2 AMI > select t2.micro > Next: Configure instance Details<br>

Network: change it to myVPC > for the Subnet, select Subnet 2 > Next : Add Storage (leave as it is by default) <br>

Next: Add Tags > Key: Name, Value: myDataBaseServer > Next: Configure Security Group > Select an existing security group<br>

Select "default VPC security group" > Review and Launch > Choose an existing key pair: select KP > Launch instances<br>

Now we should have 2 running `EC2` instances, one for our <b>Public subnet</b> and the other for our <b>Private subnet</b>.

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-67.png](https://i.postimg.cc/bvF73J2g/isaac-arnault-AWS-67.png)](https://postimg.cc/zLK2fq7H)

</p>
</details>

## Part 4 : let's create a new Security Group for our Database Server

Services > EC2 > Security groups > Create security group <br>

Security group name: myDB-SG, Description: My Database Security Group<br>

VPC: choose "myVPC"<br>

Add Rule: select "ALL ICMP IPv4", Source: 10.0.1.0/24 <br>

Add Rule: select "SSH", Source: 10.0.1.0/24 <br>

Add Rule: select "HTTP", Source: 10.0.1.0/24 <br>

Add Rule: select "HTTPS", Source: 10.0.1.0/24 <br>

Add Rule: select "SSH", Source: 10.0.1.0/24 <br>

Add Rule: select "MYSQL/Aurora", Source: 10.0.1.0/24 <br>

Click Create. We now have two provisioned Security Groups, <b>mySG</b> and <b>myDB-SG</b>.

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-72.png](https://i.postimg.cc/qRy7tL4V/isaac-arnault-AWS-72.png)](https://postimg.cc/tZRbwFs2)

</p>
</details>

Go to EC2 and assign a new Securtity Group to "myDataBaseServer":<br>

Click on myDataBaseServer > Actions > Networking > Change Security Groups<br>

Unselect default VPC > Select myDB-SG > Click "Assign Security Groups"<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-73.png](https://i.postimg.cc/BbPBPRtZ/isaac-arnault-AWS-73.png)](https://postimg.cc/p5xFgGD3)

</p>
</details>

Copy to the clipboard the Private IP address of "MyDatabaseServer"<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-73.png](https://i.postimg.cc/BbPBPRtZ/isaac-arnault-AWS-73.png)](https://postimg.cc/p5xFgGD3)

</p>
</details>


## Part 5 : Let's perform some tests

### 5.1 let's connect to our EC2 instances using SSH

Ctrl + Alt +t to open a new `CLI`.<br>

We enter the folder where we have placed our <b>KP.pem</b> file (we downloaded this file while setting up our first EC2 instance).<br>

Use the following commands: <br>

`$ chmod 400 KP.pem` - to grant access to our <b>KP.pem</b><br>

`$ ssh ec2-user@WebServer-1_IPv4_Address -i KP.pem`<br>

Type "yes" when prompted by the `CLI`<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-67.png](https://i.postimg.cc/bvF73J2g/isaac-arnault-AWS-67.png)](https://postimg.cc/zLK2fq7H)

</p>
</details>

### 5.1 let's see if the two EC2 instances communicate with each other

<b>Method 1 : ping Server 2 in SSH from Server 1</b>

One is on a public subnet, the other one on a private subnet.<br>

On your `CLI`, connect to <b>WebServer-1</b> in `SSH` in order to ping <b>myDatabaseServer</b><br>

`$ ssh ec2-user@WebServer-1_IPv4_Address -i KP.pem`<br>

`$ ping myDatabaseServer_private_IP`

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-77.png](https://i.postimg.cc/7hvfmLqz/isaac-arnault-AWS-77.png)](https://postimg.cc/FdZrKNdF)

</p>
</details>

Do not close your CLI.

<b>Method 2: copy the content of the <b>KP.pem</b> file</b>

In a new CLI, use as follows: <br>

Place yourself to the root of the .pem file and use `$ nano KP.pem`<br>

Copy to your clipboard the content of the file.<br>

Go back to your CLI (see Method 1) and use as follows : <br>

`$ nano PVKEY.pem` - to create a new file, and paste the content of KP.pem file in there.<br>

`$ Ctrl + x` then `y` to save and exit.<br>

`$ chmod 400 PVKEY.pem` - to grant access to your file<br>

Copy the IP address of "myDataBaseServer" and use it as follows:<br>

`$ ssh ec2-user@myDatabaseServer_private_IP -i PVKEY.pem` - to connect to "myDataBaseServer" from "WebServer-1"<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-78.png](https://i.postimg.cc/J09vs9cM/isaac-arnault-AWS-78.png)](https://postimg.cc/m1y8qp55)

</p>
</details>

## Part 6 : Install a NAT gateway
The purpose of installing a NAT gateway is to enable and allow our `EC2` instances and Private subnet to go out of the VPC and download softwares.<br>

To do that they need to communicate to the `Internet Gateway` that we've installed.<br>

Go to Services > EC2 > Launch Instance > Go to Community AMIs > Search for "nat"<br>

Select "amzn-ami-vpc-nat-hvm-2018.03.0.20181116-x86_64-ebs"<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-80.png](https://i.postimg.cc/7Zjj4tq4/isaac-arnault-AWS-80.png)](https://postimg.cc/QFkfkbBY)

</p>
</details>

- Next : Configure Instance Details > change Network to "myVPC"<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-81.png](https://i.postimg.cc/sx0wc1Xz/isaac-arnault-AWS-81.png)](https://postimg.cc/q6ysBJyD)

</p>
</details>

- Next: Add Storage (leave as it is by default) > Next: Add Tags > Add Tag: Name, Value: NAT_Instance<br>

- Configure Security Groups > Select an existing Security Group > Select <b>mySG</b> Security Group > Review and Launch<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-82.png](https://i.postimg.cc/xT1dN8MC/isaac-arnault-AWS-82.png)](https://postimg.cc/G96RZcMw)

</p>
</details>

- Boot from General Purpose (SSD): choose "Make General Purpose (SSD) the boot volume for this instance."<br>

- Launch Instance<br> Choose an existing Key Pair: select "KP" > Launch Instances.<br>

- Check that your instance is correctly running: <br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-84.png](https://i.postimg.cc/X72Dnjwd/isaac-arnault-AWS-84.png)](https://postimg.cc/svhJcRHg)

</p>
</details>

- We need to change the Source and Destination Check on our NAT instance:<br>

- Click on your <b>NAT_Instance</b> > Actions > Networking > Change Source / Dest. Check > click "Yes, Disable"

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-85.png](https://i.postimg.cc/L6sNCcrX/isaac-arnault-AWS-85.png)](https://postimg.cc/bdKxdBYc)

</p>
</details>

To allow our EC2 instances to talk to our NAT instance, we need to create a new route on our `VPC`.<br>

Go to Services > Networking & Content Delivery > VPC > Route tables > Select 2nd Route of our `VPC`

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-85.png](https://i.postimg.cc/L6sNCcrX/isaac-arnault-AWS-85.png)](https://postimg.cc/bdKxdBYc)

</p>
</details>

> Click Routes > Edit routes > Add route > Destination: 0.0.0.0/0 > Target: Instance > Select NAT_Instance > Save Route<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-87.png](https://i.postimg.cc/ryRPqXfP/isaac-arnault-AWS-87.png)](https://postimg.cc/grdDK5FV)

</p>
</details>

Go to Services > EC2 > Copy to your clipboard `IPv4 Public IP` of <b>WebServer-1</b><br>

SSH to that public address <br>

Connect to the `Private IP` of <b>myDataBaseServer</b> using `SSH`.

<details>
<summary>🔴 See output</summary>
<p> 

[![isaac-arnault-AWS-88.png](https://i.postimg.cc/DZ4QqhDJ/isaac-arnault-AWS-88.png)](https://postimg.cc/xJYb2w9n)

</p>
</details>

Let's perform a `$ yum update -y` while being connected in SSH to our IP adress of <b>myDataBaseServer</b>.<br>

If updates perform, it means that everything is set up correctly and that your `EC2` instances use our `NAT` Instance to connect to the Internet.


<details>
<summary>🔴 See output</summary>
<p> 

[![isaac-arnault-AWS-89.png](https://i.postimg.cc/ZnbTG8Nr/isaac-arnault-AWS-89.png)](https://postimg.cc/1ndh6NJt)

</p>
</details>





