# AWS 3 Tier Architecture
A Three-Tiered Application for hosting Static UI, backed Micro-Service and a Database Services on AWS Cloud


##  AWS Services Used 

- Application Load Balancer 
- Classic Load Balancer 
- EC2 Instances 
- Amazon Document DB (Mongo) 
- Amazon RDS (PostGress) 
- AWS CloudWatch 
- AWS CloudTrail 
- AWS IAM 
- AWS VPC 


## VPC Setup

9 Subnets in 3 Availability Zones

### Public Subnet
  - `Components` : Application Load Balancer and NAT Gateway
  - `Routing` : Intrenal to VPC through Route Table and a Internet Gateway for Public Traffic

### Application Subnet
  - `Components` : Classic Load Balancer and NAT Gateway.
  - `Routing` : Intrenal to VPC through Route Table.

### Database Subnet
  - `Components` : AWS Document Database and AWS RDS.
  - `Routing` : Intrenal to VPC through Route Table.


## Netwoking Setup


### Application Load Balancer (L7)

  - `Security Groups From Internet on Port 443 `
  - `Communication Protocol -> HTTPS`
  -  `SSL Manadatory`  

### FrontEnd VM's

  - `Security Groups to Allow from Application Load Balancer on Port 443 `
  - `Communication Protocol -> HTTPS`
  -  `SSL Mandatory`  


### Internal Load Balancer (L4)

  - `Security Groups to Allow from FrontEnd VM on Port 443 `
  - `Communication Protocol -> HTTPS`
  -  `SSL Optional`  

### Backend VM's 

  - `Security Groups to Allow from Internal Load Balancer on Port 80 `
  - `Communication Protocol -> HTTP`
  -  `SSL Optional`  

### Database Subnet 


#### Amazon DocumentDB ( MangoDB)
-  `Security Groups to Allow from Backend VM’s on Port 27017 `
-  `Communication Protocol -> TCP / SSL`

#### Amazon RDS ( For postGress)
- `Security Groups to Allow TCP Traffic on Port from Backend VM’s on Port 5432`
- `Communication Protocol -> TCP / SSL`



## Change Log
