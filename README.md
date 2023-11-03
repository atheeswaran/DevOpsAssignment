**DevOpsAssignment**

Deployment of Jenkins LTS solution for achieving Continuous Build for a software. 

**Problem statement:**

Perform a Jenkins LTS Deployment and install the plugin of Git and Maven. After successful deployment change the access port for Jenkins from 8080 (default) to 9090. Also list the need and benefits of Jenkins. 

**Prerequisites:**

1. **AWS Account**: Access to AWS account and EC2 instances (Jenkins and Tomcat installations) running.
2. **GITHub Account**: Access to GitHub account to push code and poll from Jenkins as part of Continuous Build/Integration

**Assignment Links:**

1. **Jenkins AWS EC2 instance** => http://ec2-52-90-239-234.compute-1.amazonaws.com:8080/
2. **Tomcat deployment EC2 instance** => http://ec2-54-90-103-163.compute-1.amazonaws.com:8080/service/
3. **GitHub URL with Maven based Java web project** => https://github.com/atheeswaran/DevOpsAssignment/

**Step 1: EC2 Instance Setup**

1. Login to AWS and launch instance for Jenkins deployment
    => create Linux AMI and select t2.micro as instance type
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
3. Open Jenkins hosted EC2 url
   => http://ec2-52-90-239-234.compute-1.amazonaws.com:8080/
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/da4435fe-5ed2-4dac-9439-ba17dca16437)
4. Set InitialAdmin Password and login with credentials
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/c9aade89-2124-446e-8fce-5b65bc5afcf9)
5. Configure Jenkins via Manage Jenkins => Tools option
   1) JDK - JAVA_HOME
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/40ba405f-ad04-4499-bd14-adf7f27c4a63)
   2) GIT - installation path on ec2
      ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/893ce299-022b-4b6f-a35a-661a47421238)
   3) Maven - MAVEN_HOME
      ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/06f453f0-a4d7-4804-bcf7-538c8dcb3c47)
6. install "Deploy to container plugin"
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/302d3f1a-0979-455c-a404-69c54cdec83e)


**Step4: Jenkins - New Job:**

1. **Click New Item** => "javawebautodeploy" > select Freestyle Project
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/2a4ce14a-d7c1-4534-bfd0-6ba5b8650ffb)
2. **Setup Source code management - GIT**
   1. provide repository URL => https://github.com/atheeswaran/DevOpsAssignment/
   2. add GITHub credentials (in order to pull code from GIT automatically)
![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/c5038ce9-582b-4270-a3f5-163a12d6583c)
3. **Build Triggers** => poll GITHub changes and push code automatically in particular interval of time
   in this case => it is " ****" => to poll changes for every minute
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/3c128d5d-319e-4c7c-ae8b-ded9f91ba592)
4. **Build Steps - Maven:**
   => Maven and "Clean package" as Goals. see below
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/9ae62780-f265-4615-b7fb-8829141f5cee)
5. **Post-Build Actions:**
   => add postbuild action with "deploy war/ear to a container" option
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/e236735c-78ce-4cac-bda2-643aecb9bf2f)   
   => war and context path
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/359a59a0-e3eb-440a-8151-6b1b17f37913)
   => Provide tomcat URL with credentials (deployer user) (Step 5 point 6 is pre-req => check below)
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/b389e22e-871b-497a-afbb-b0d592aa3389)

**Step 5: Tomcat Setup**

1. Launch new EC2 instance and connect to linux terminal
   => switch to root user by using sudo -i command
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/8d02ad0e-e5e3-4879-b8e0-7e9c3446bccd)
2. install Tomcat
   => by using yum -y install tomcat9
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/cc156d4a-e94d-40c9-ba0f-18a0023939b7)
3. start Tomcat service
   => by using service tomcat9 start
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/3cf8617a-aa30-48a6-91aa-677671957237)
4. Open EC2 Tomcat URL
   => http://ec2-54-90-103-163.compute-1.amazonaws.com:8080/
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/4d3490b4-4f6d-4844-8c29-b8d48a35ab75)
5. install tomcat9 webapps  
   => yum install tomcat9-webapps tomcat9-admin-webapps
6. Edit tomcat-users.xml to add new user "**deployer**" to deploy "war/jar" with right access later
   => edit /usr/share/tomcat9/conf/tomcat-users.xml
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/293376dc-e2be-4340-b2c5-1a92731037ea)
7. update tomcat-users.xml with admin user inorder to use "Manager App" in tomcat webpage
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/9a10c015-c783-48f5-ba13-9c17cc333b7d)

**Step 6: Code (Maven based javawebapp) push to GITHub:**
1. **Create Maven Project with below Archetype** => archetype-webapp
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/29fade3e-cbb2-413e-a35a-60356d601651)
2. **Edit pom.xml** to indicate Maven plugin, target directory paths
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/1afdcc67-1f1a-41bc-8a2a-07bbfaecab85)
3.** Edit index.jsp** like below
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/8783082b-959a-4fcb-b8c2-9cadafcde3e2)
4. **Edit webapp** displayname in Web.xml like below
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/85074fb4-caa4-4c0f-8555-a0d695b97ec8)
5. **Commit and push to GITHub repo**
   => https://github.com/atheeswaran/DevOpsAssignment
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/36486e75-8b4f-419d-a30b-8618859af02e)

**Step 7: Continous Integration /Deployment**
1. Make changes to index.jsp in maven project
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/c8f596f4-fab0-431a-9ec1-af5f1f7a9854)
2. push the changes to GITHub
3. check Jenkins Dashboard > javawebautodeploy job for automatic build
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/23657c8e-2073-4dc0-8629-3985f5e5bf50)
4. Open tomcat (http://ec2-54-90-103-163.compute-1.amazonaws.com:8080/) > click "manager App"
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/ad9cbd50-7b7a-44a8-8483-9e361999d866)
5. Click "service" application and see the latest changes in "index.jsp"
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/9dc7096d-a630-4017-bb50-17fafbec3d39)


**After successful deployment change the access port for Jenkins from 8080 (default) to 9090:**
1. Edit "/usr/lib/systemd/system/jenkins.service"
2. update Jenkins_PORT = 9090 instead of "8080"
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/0ba8b8f0-dca1-4337-877a-7e9f4d63472e)
3. restart Jenkins service
   => using service jenkins start
   ![image](https://github.com/atheeswaran/DevOpsAssignment/assets/19812046/2668045b-146f-4244-8dca-f82ac8e36668)
4. Run Jenkins on 9090 and check if its successful

**Need and Benefits of Jenkins:**

1.**Need of Jenkins:**

   a) **Automation**: Jenkins automates building and deployment processes,avoiding the need for manual intervention and minimizing errors.
   b) **Continuous Integration/Delivery**: It integrates with various version control systems like Git, enabling continuous integration and continuous delivery (CI/CD) pipelines.
   C) **wide range of Plugins**: with help of plugins, Jenkins allows seamless integration with other tools used in the development lifecycle.
   d) **Monitoring and Reporting**: Jenkins provides detailed logs and reports, allowing developers to monitor the progress of builds and deployments.
   e) **Need of Collaboration**: Jenkins facilitates collaboration among development and operations teams to improve workflows.

2. **Benefits of Jenkins:**   
   a) **Faster Development**: By automating repetitive tasks, Jenkins speeds up the development process, enabling faster deployment.
   b) **Reliability**: Automated builds and tests ensure consistency and reliability thereby reducing the chances of errors and bugs in product.
   c) **Cost-Efficiency:** Automation reduces the need for manual labor, saving time and resources, ultimately leading to cost savings.
   d) **Scalability**: Jenkins can handle multiple projects simultaneously, making it scalable for both small and large development teams.
   e) **Flexibility**: Jenkins supports a wide range of plugins/integrations, allowing developers to use their preferred tools/technologies seamlessly.
   f) **Enhanced Collaboration**: Jenkins promotes collaboration between development, testing, and operations teams, fostering a culture of shared responsibility and teamwork.



   
   




   



   




   

   








      


   









