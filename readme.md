# **High Availability Deployment Using Auto Scaling Group and Load Balancer**

## 📝 **Introduction**

This project demonstrates the setup of an Auto Scaling Group (ASG) integrated with an Application Load Balancer (ALB) on AWS. The goal is to ensure high availability, scalability, and fault tolerance for deployed applications

## 🚀 **Architecture Overview**

Application Load Balancer (ALB) distributes incoming traffic across healthy instances.

Target Group registers instances created by the ASG.

Launch Template/Launch Configuration defines EC2 instance settings (AMI, instance type, security group, key pair).

Auto Scaling Group (ASG) manages scaling policies based on demand (CPU utilization, request count, etc).


## 📋 **Prerequisites**

• AWS Account

• IAM role with required permissions

• Amazon VPC with public/private subnets

• Key Pair for EC2 access

• Security Groups for ALB and EC2


## ⚙ **Steps to Deploy**

 **Step1 - Launch template**

• Create launch Template.

![alt text](<ASG (2)-1.png>)

• Attach Security Group (allow SSH/HTTP).

![alt text](<ASG (2)-1-1.png>)

• Add User Data.

![alt text](<ASG (3)-1.png>)

• Launch Three sets of template (Home,Laptop,Mobile).

![alt text](<ASG (4)-1.png>)

 **Step2- Create Auto Scaling Groups (ASG)**

a) Home ASG (Static Scaling)

• Launch configuration / Launch template with Amazon Linux 2 AMI.

![alt text](<ASG (5)-1.png>)

• Select Availability Zone and subnets

![alt text](<ASG (6)-1.png>)

• Fixed capacity (e.g., Desired = 2, Min = 2, Max = 2).

![alt text](<ASG (7)-1.png>)

• Create Auto Scaling Group.
 
 • Review

![alt text](<ASG (35)-1.png>)


b) Laptop ASG (Dynamic Scaling)

• Launch configuration / Launch template.

![alt text](<ASG (8)-1.png>)

• Set Desired = 3, Min = 2, Max = 7.

![alt text](<ASG (10)-1.png>)


• Add scaling policy:

![alt text](<ASG (11)-1.png>)

• Review

![alt text](<ASG (36)-1.png>)

c) Mobile ASG (Scheduled Scaling)

• Launch configuration / Launch template.

![alt text](<ASG (9)-1.png>)

• Set Desired = 3, Min = 2, Max = 7.

![alt text](<ASG (10)-1-1.png>)

• Add schedule policy:

![alt text](<ASG (10)-1-2.png>)

• Set Scheduled Action(Mobile)

• Select Mobile ASG.

![alt text](<ASG (18)-1.png>)

• Review

![alt text](<ASG (37)-1.png>)

• Create Schedule Action

![alt text](<ASG (19)-1.png>)

• Set Desired = 8, Min = 5, Max = 15.

![alt text](<ASG (20)-1.png>)

• Review 

![alt text](<ASG (21)-1.png>)

 • Launch Three sets of Auto Scaling Groups (Home,Laptop,Mobile).

![alt text](<ASG (12)-1.png>)

**Step3 - Create Target Groups**

• Create Target group (Home).

![alt text](<ASG (13)-1.png>)

• Create Target Group(Laptop).

![alt text](<ASG (14)-1.png>)

• Set health Checks.

![alt text](<ASG (15)-1.png>)

• Create Target Group(Mobile).

![alt text](<ASG (16)-1.png>)

• verify three Target Groups(Home,Laptop,Mobile).

![alt text](<ASG (17)-1.png>)

**Step4 - Create Application Load Balancer (ALB)**

• Load Balancers → Create Load Balancer.

![alt text](<ASG (38)-1.png>)

• Choose Application Load Balancer.

![alt text](<ASG (40)-1.png>)

Configure:

• Listeners: HTTP on port 80

![alt text](<ASG (42)-1.png>)

• Under Listeners and Routing:

      Forward /home path → Home-TG

      Forward /laptop path → Laptop-TG

      Forward /mobile path → Mobile-TG

![alt text](<ASG (29)-1.png>)

## ✅ **Verification**

• Get ALB DNS name from Load Balancer.

![alt text](<ASG (30)-1.png>)

• Test in browser:

• http://<ALB-DNS>/home → Routes to Home ASG instances.

![alt text](<ASG (31)-1.png>)

• http://<ALB-DNS>/laptop → Routes to Laptop ASG instances.

![alt text](<ASG (32)-1.png>)

• http://<ALB-DNS>/mobile → Routes to Mobile ASG instances.

![alt text](<ASG (33)-1.png>)


## 📖 **Summary**

ALB distributes traffic to different Target Groups.

Home ASG → Static scaling.

Laptop ASG → Dynamic scaling.

Mobile ASG → Scheduled scaling.

This setup ensures high availability, cost optimization, and performance across different application services.










