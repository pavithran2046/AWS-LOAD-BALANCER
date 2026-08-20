# AWS-LOAD-BALANCER



## AIM
To use Elastic Load Balancing (ELB) and Auto Scaling services to load balance and automatically scale an AWS infrastructure.

## ALGORITHM
## Step 1: Create an AMI for Auto Scaling
Open the EC2 console, confirm that Web Server 1 is running (2/2 status checks passed), select the instance, and choose Actions → Image and templates → Create image. Name it "WebServerAMI" and create it. This AMI will be used to launch identical instances later.

## Step 2: Create a Target Group and Load Balancer
Create a Target Group named "LabGroup" (type: Instances, VPC: Lab VPC) without registering targets yet. Then create an Application Load Balancer named "LabELB" under Lab VPC, mapped to Public Subnet 1 and Public Subnet 2, using the Web Security Group, with the HTTP:80 listener forwarding to LabGroup.

## Step 3: Create a Launch Template and Auto Scaling Group
Create a Launch Template named "LabConfig" using the WebServerAMI, instance type t2.micro, key pair "vockey", the Web Security Group, and Detailed CloudWatch monitoring enabled. Using this template, create an Auto Scaling group named "Lab Auto Scaling Group" attached to Private Subnet 1 and Private Subnet 2, linked to the LabGroup target group, with desired/minimum/maximum capacity of 2/2/6 and a target tracking scaling policy set to maintain 60% average CPU utilization.

## Step 4: Verify Load Balancing
Confirm that two new "Lab Instance" EC2 instances were launched by Auto Scaling and that both show a "healthy" status in the LabGroup target group. Copy the Load Balancer's DNS name and open it in a browser to confirm the application is being served correctly through the load balancer.

## Step 5: Test Auto Scaling
Lower the scaling policy's target CPU value to 50% to make scaling trigger sooner, then use the application's "Load Test" feature to generate high CPU load across the instances. Monitor the CloudWatch alarms (AlarmLow/AlarmHigh) until AlarmHigh enters the "In alarm" state, then verify in the EC2 console that additional instances were automatically launched to handle the load.

## Step 6: Terminate the Original Web Server
Select Web Server 1 (the original instance used to create the AMI) and terminate it, since it is no longer needed once the Auto Scaling group is managing instances independently.

## COMMANDS
No CLI commands are used in this experiment, as it is performed entirely through the AWS Management Console (GUI-based setup) using EC2, Elastic Load Balancing, Auto Scaling, and CloudWatch services.

## OUTPUT

<img width="1337" height="572" alt="image" src="https://github.com/user-attachments/assets/ea14d7ad-e09e-4a3a-9406-c584a5d83543" />
<img width="1333" height="575" alt="image" src="https://github.com/user-attachments/assets/459ec264-f4ed-4100-b1ee-fa50dc0a7db9" />
<img width="1336" height="573" alt="image" src="https://github.com/user-attachments/assets/b6b244de-63cd-43ba-9817-c2630ed5e4c0" />
<img width="1341" height="572" alt="image" src="https://github.com/user-attachments/assets/3dac999c-28e4-45e0-aa2b-c7be1f9caffb" />
<img width="1337" height="572" alt="image" src="https://github.com/user-attachments/assets/9fd5f77b-662b-42a7-a0b4-49be9d587350" />
<img width="1335" height="575" alt="image" src="https://github.com/user-attachments/assets/a88d01c7-0ea8-46a4-887c-492b311d5c28" />
<img width="1332" height="575" alt="image" src="https://github.com/user-attachments/assets/fa4f2b55-b48b-44b8-9772-d6d360a1ed39" />
<img width="1342" height="577" alt="image" src="https://github.com/user-attachments/assets/5bbf17fc-20ea-404e-908b-f1d6a34143a2" />
<img width="1332" height="575" alt="image" src="https://github.com/user-attachments/assets/46984b10-6314-4d48-a0c2-8bc6fd85340f" />
<img width="1332" height="576" alt="image" src="https://github.com/user-attachments/assets/9801f078-b707-476b-a259-f3a24d668d0e" />
<img width="1336" height="553" alt="image" src="https://github.com/user-attachments/assets/c6a87c1e-a230-49da-840a-01329cbf612d" />
<img width="1251" height="656" alt="image" src="https://github.com/user-attachments/assets/066f5dd7-855e-457b-a438-fb289e1e5aeb" />
<img width="1342" height="556" alt="image" src="https://github.com/user-attachments/assets/48a96b89-b28a-49b7-9767-e9b5c2d1b467" />
<img width="1337" height="550" alt="image" src="https://github.com/user-attachments/assets/b428dd5a-59ab-426e-8869-05b743af23ed" />
<img width="1338" height="577" alt="image" src="https://github.com/user-attachments/assets/036745cd-17ae-44eb-ac26-ea45c4b8ee9d" />
<img width="1342" height="553" alt="image" src="https://github.com/user-attachments/assets/19e90ebf-8ae8-44ea-a6cc-e03a9518ed9b" />
<img width="1330" height="612" alt="image" src="https://github.com/user-attachments/assets/bda1e29e-074e-4dc6-a158-1cd38534a15c" />


## RESULT
Thus, an AMI was created from a running EC2 instance, a Load Balancer was configured to distribute traffic across multiple instances, an Auto Scaling group was set up with a target tracking scaling policy, and the infrastructure was verified to automatically scale out under increased load using CloudWatch alarms.



