**DevOpsAssignment**
Deployment of Jenkins LTS solution for achieving Continuous Build for a software. 

**Problem statement: **
Perform a Jenkins LTS Deployment and install the plugin of Git and Maven. After successful deployment change the access port for Jenkins from 8080 (default) to 9090. Also list the need and benefits of Jenkins. 

**Prerequisites:**
1. **AWS Account**: Access to AWS account and EC2 instances (Jenkins and Tomcat installations) running.
2.** GITHub Account**: Access to GitHub account to push code and poll from Jenkins as part of Continuous Build/Integration

**Assignment Links:**
1. **Jenkins AWS EC2 instance** => http://ec2-174-129-106-139.compute-1.amazonaws.com:8080/
2.** Tomcat deployment EC2 instance** => http://ec2-52-91-54-187.compute-1.amazonaws.com:8080/service/
3.** GitHub URL with Maven based Java web project** => https://github.com/atheeswaran/DevOpsAssignment/

**Step 1: EC2 Instance Setup**
1. Login to AWS and launch instance for Jenkins deployment
    => create Linux AMI and select t2.micro type
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/7047d291-a2d7-4870-839b-7a2a9335ce32)
3. Edit inbound rules and update with Port "8080"
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/2cebbedd-7f7e-44ba-a7e1-cd7c2ef9f88d)
4. Connect to EC2 instance and launch Linux terminal
   => switch to root user by using sudo -i command
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/060dead0-2547-486c-88a6-6ab166d811b0)

Step2: 




