**DevOpsAssignment**
Deployment of Jenkins LTS solution for achieving Continuous Build for a software. 

**Problem statement:**
Perform a Jenkins LTS Deployment and install the plugin of Git and Maven. After successful deployment change the access port for Jenkins from 8080 (default) to 9090. Also list the need and benefits of Jenkins. 

**Prerequisites:**
1. **AWS Account**: Access to AWS account and EC2 instances (Jenkins and Tomcat installations) running.
2. **GITHub Account**: Access to GitHub account to push code and poll from Jenkins as part of Continuous Build/Integration

**Assignment Links:**
1. **Jenkins AWS EC2 instance** => http://ec2-52-90-239-234.compute-1.amazonaws.com:8080/
2. **Tomcat deployment EC2 instance** => http://ec2-52-91-54-187.compute-1.amazonaws.com:8080/service/
3. **GitHub URL with Maven based Java web project** => https://github.com/atheeswaran/DevOpsAssignment/

**Step 1: EC2 Instance Setup**
1. Login to AWS and launch instance for Jenkins deployment
    => create Linux AMI and select t2.micro type
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/7047d291-a2d7-4870-839b-7a2a9335ce32)
3. Edit inbound rules and update with Port "8080"
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/2cebbedd-7f7e-44ba-a7e1-cd7c2ef9f88d)
4. Connect to EC2 instance and launch Linux terminal
   => switch to root user by using sudo -i command
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/060dead0-2547-486c-88a6-6ab166d811b0)

**Step2: Install Required Plugins**
1. Install JDK
   => use yum -y install java
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/307d2377-7a8f-4f57-a38b-6d146b77aaff)
2. Install GIT
   => use yum -y install GIT
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/33c6ba65-95c1-42d0-bb7b-18f5974d38a7)
3. Install Maven
   => use yum -y install maven
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/429b0a44-e570-40d0-8ba1-29a530584cd5)

**Step3: Jenkins setup**
1. Install Jenkins
   => use yum -y install Jenkins
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/efe1c585-cce8-462b-b125-177dae649d4e)
2. Start Jenkins
   => use service jenkins start
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/04fcba47-c4da-48b7-8ebc-958337ac4876)
3. 







