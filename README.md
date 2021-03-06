# CLOUDFORMATION-MySQLWebApp

## Description:
	 
	This is a Cloudformation template for configuring MySQL in an instance and access it through a server
	placed in a Public Subnet. The MySQL Database is kept private and is accessed through the public
	instances. Load balancers and Autoscaling groups are configured accordingly.
	

## INFRASTRUCTURE DIAGRAM: 

![alt text](AWS-Infra-diag.jpg)

## Files

	This repository contains 4 files. Each stack is dependent on the other so they must be uploaded in
	the given order.
		1. StackVPC
		2. StackInstance
		3. StackLB
		4. StackAsg

### 1. StackVPC
	In this file, a VPC is defined containing 3 subnets. Two of them are public and one is private.
	An internet gateway is attached to the public subnets and NAT gateway is attached to the private
	subnet. Routes were configured accordingly. The resources in the private subnet can only be 
	accessed through the public subnet. The network access control list is also defined which 
	whitelists all the IPs and can be edited to control access through any IP. Parameterization has 
	been done accordingly and are to be set according to the needs of the infrastructure.

### 2. StackInstance

	The Private Instance is configured in this file. A MySQL server is configured in the instance.
	The username and password are pre-configured as admin and password respectively but can be
	changed accordingly.

### 3. StackLB

	The load balancer is configured in this file. It is a classic load balancer. It re-routes the 
	port 80 traffic of the Public instances. It is configured to operate in the public and private
	subnets. Health checks are also set inside the load balancer. Parameterization has been 
	done accordingly and are to be set according to the needs of the infrastructure.

### 4. StackAsg

	The launch configuration along with the auto-scaling groups of public and private instances.
	The public instance launch configurationis set to access the MySQL database server using the
	username and password of admin and password respectively. Theautoscaling group of public
	instance is Multi-AZ attached to the load balancer. It has a max and min size of 4 and 2
	respectively. Parameterization has been done accordingly and are to be set according to the
	needs of the infrastructure.

### 5. StackMaster(Optional)
	The whole process can be automated if the four files above are uploaded online and the links
	are to be added to this file. If automated, only this file must be uploaded. Parameterization
	has been done accordingly and are to be set according to the needs of the infrastructure.

