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

![alt text](<Screenshot 2025-09-25 220414.png>)

• Attach Security Group (allow SSH/HTTP).

![alt text](<Screenshot 2025-09-25 220550.png>)

• Add User Data.

![alt text](<Screenshot 2025-09-25 220620.png>)

• Launch Three sets of template (Home,Laptop,Mobile).

![alt text](<Screenshot 2025-09-25 223407.png>)

 **Step2- Create Auto Scaling Groups (ASG)**

a) Home ASG (Static Scaling)

• Launch configuration / Launch template with Amazon Linux 2 AMI.

![alt text](<Screenshot 2025-09-25 223955.png>)

• Select Availability Zone and subnets

![alt text](<Screenshot 2025-09-25 224053.png>)

• Fixed capacity (e.g., Desired = 2, Min = 2, Max = 2).

![alt text](<Screenshot 2025-09-25 224207.png>)

• Create Auto Scaling Group.
 
 • Review

![alt text](<Screenshot 2025-09-27 223705.png>)


b) Laptop ASG (Dynamic Scaling)

• Launch configuration / Launch template.

![alt text](<Screenshot 2025-09-25 224412.png>)


• Set Desired = 3, Min = 2, Max = 7.

![alt text](<Screenshot 2025-09-25 225146.png>)

• Add scaling policy:

![alt text](<Screenshot 2025-09-25 225353.png>)

• Review

![alt text](<Screenshot 2025-09-27 223934.png>)

c) Mobile ASG (Scheduled Scaling)

• Launch configuration / Launch template.

![alt text](<Screenshot 2025-09-25 225052.png>)

• Set Desired = 3, Min = 2, Max = 7.

![alt text](<Screenshot 2025-09-25 225146.png>)

• Add schedule policy:

![alt text](<Screenshot 2025-09-25 225353.png>)

• Set Scheduled Action(Mobile)

• Select Mobile ASG.

![alt text](<Screenshot 2025-09-25 230741.png>)

• Review

![alt text](<Screenshot 2025-09-27 224041.png>)

• Create Schedule Action

![alt text](<Screenshot 2025-09-25 231028.png>)

• Set Desired = 8, Min = 5, Max = 15.

![alt text](<Screenshot 2025-09-25 231438.png>)

![alt text](<Screenshot 2025-09-25 231709-1.png>)

• Review 

![alt text](<Screenshot 2025-09-25 231709.png>)

 • Launch Three sets of Auto Scaling Groups (Home,Laptop,Mobile).

![alt text](<Screenshot 2025-09-25 225441.png>)

**Step3 - Create Target Groups**

• Create Target group (Home).

![alt text](<Screenshot 2025-09-25 230132.png>)

• Create Target Group(Laptop).

![alt text](<Screenshot 2025-09-25 230246.png>)

• Set health Checks.

![alt text](<Screenshot 2025-09-25 230324.png>)

• Create Target Group(Mobile).

![alt text](<Screenshot 2025-09-25 230403.png>)

• verify three Target Groups(Home,Laptop,Mobile).

![alt text](<Screenshot 2025-09-25 230541.png>)

**Step4 - Create Application Load Balancer (ALB)**

• Load Balancers → Create Load Balancer.

![alt text](<Screenshot 2025-09-27 232306-1.png>)

• Choose Application Load Balancer.

![alt text](<Screenshot 2025-09-27 232353-1.png>)

Configure:

• Listeners: HTTP on port 80

![alt text](<Screenshot 2025-09-27 232533-1.png>)

• Under Listeners and Routing:

      Forward /home path → Home-TG

      Forward /laptop path → Laptop-TG

      Forward /mobile path → Mobile-TG

![alt text](<Screenshot 2025-09-25 232950-1.png>)

## ✅ **Verification**

• Get ALB DNS name from Load Balancer.

![alt text](<Screenshot 2025-09-25 233020.png>)

• Test in browser:

• http://<ALB-DNS>/home → Routes to Home ASG instances.

![alt text](<Screenshot 2025-09-26 145517.png>)

• http://<ALB-DNS>/laptop → Routes to Laptop ASG instances.

![alt text](<Screenshot 2025-09-26 145732.png>)

• http://<ALB-DNS>/mobile → Routes to Mobile ASG instances.

![alt text](<Screenshot 2025-09-26 145826.png>)

## 📖 **Summary**

ALB distributes traffic to different Target Groups.

Home ASG → Static scaling.

Laptop ASG → Dynamic scaling.

Mobile ASG → Scheduled scaling.

This setup ensures high availability, cost optimization, and performance across different application services.










