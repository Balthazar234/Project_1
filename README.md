<h1>Jenkins CI/CD pipeline with GitHub webhook integration for Deploying Docker application on EC2 instances using the declarative pipeline.</h1>

<h2>Description</h2>
Automating Deployment with Jenkins CI/CD and Docker on AWS EC2: This project demonstrates a seamless CI/CD pipeline using Jenkins with GitHub webhook integration. It deploys Docker applications on EC2 instances using a declarative pipeline, streamlining the development-to-production process.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Public Cloud Service(AWS)</b> 

<h2>Environments Used </h2>

- <b>Ubuntu EC2 Instance</b>

<h2>Program walk-through:</h2>

<p align="center">
Follow the steps:

1. First of all, go to the AWS portal, and create a new instance. As,

· Name: jenkins-server

· AMI: ubuntu.

· Instance type: t2.micro (free tier).

· Key pair login: Create > docker.pem.

· Allow HTTP.

· Allow HTTPS.

(Download the .pem file.)

Click on Launch Instance. <br/>
<img src="https://i.imgur.com/dIXrZSx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
2. Now, connect to the EC2 instance that you have created. Copy the SSH from server:  <br/>
<img src="https://i.imgur.com/bDJyDRx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
3. Go to the download folder, where the .pem file is placed and open the terminal in the same location, and paste the SSH.

4. In the machine, run the command

“ssh-keygen”

This will generate public and private keys in the machine.

Id_rsa — Private Key.

Id_rsa.pub — Public Key. <br/>
<img src="https://i.imgur.com/9PDvsna.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
5. Now we will install Jenkins on the machine, by following this link

https://www.jenkins.io/doc/book/installing/linux/

This will automatically install java with Jenkins.

6. Install Docker as well to the machine by running,

“Sudo apt-install docker.io”

7. Now check if it got installed by running “jenkins — version” and “docker — version”
 <br/>
<img src="https://i.imgur.com/EBbdEws.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
8. Now, we will allow ports 8080 and 8001 for this machine from a security group. We can find the security group in the VM description. 
Now, here we need to allow “Inbound Rule” as below: <br/>
<img src="https://i.imgur.com/mY6LpBN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
9. Now, Copy the Public Ip of the machine and paste it to the browser to access the Jenkins portal. As,

“54.193.49.139:8080” <br/>
<img src="https://i.imgur.com/C6sWPB3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

10. We need an Administrator Password to unlock this. For that, go to the provided highlighted path in the upper screenshot.

“cat /var/lib/Jenkins/secrets/initialAdminPassword” <br/>
<img src="https://i.imgur.com/txPljSa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 11. Now Click on, “Install Suggested Plugins” <br/>
<img src="https://i.imgur.com/hdH1Bgp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

12. This will now install the suggested plugins. As <br/>
<img src="https://i.imgur.com/FhbOG3O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

13. Now, Jenkins will ask us to create the First Admin User. <br/>
<img src="https://i.imgur.com/jLkiyrT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
14. Add the fields accordingly. <br/>
<img src="https://i.imgur.com/m40JRbv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />

15. The Jenkins homepage will look like this, <br/>
<img src="https://i.imgur.com/bHBU6gP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

16. Now, we will create a CI/CD pipeline, which will fetch the code from GitHub. <br/>
<br />

17. From Jenkins Dashboard, Click on “New Item”. <br/>
<img src="https://i.imgur.com/Ar71fAf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<br />

18. Now, Add the name as

Name: todo-app

Project: Freestyle project

Click “Ok”. <br/>
<img src="https://i.imgur.com/MJC1R5L.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<br />

19. Here, we need to fill up the description. <br/>
<img src="https://i.imgur.com/NBBwBap.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<br />

20. In Source Code Management, select Git and Add Repository URL and Credentials.

(If there is not any added credential, we need to add) <br/>
<img src="https://i.imgur.com/YyXhmM1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<br />

21. In Build Step, select Execute Shell and write the following command to build Docker image and from Docker image, we will create a container. <br/>
<img src="https://i.imgur.com/lVCQm3m.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<br />

22. Now, Click on Build Now. And the build will be started, in the build history. <br/>
<img src="https://i.imgur.com/uzFy2dx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<br />

23. In Output Console, <br/>
<img src="https://i.imgur.com/WqiSOEg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<br />

24. After getting success, In the browser, search for

<public_ip_of_ec2:8001> <br/>
<img src="https://i.imgur.com/sgTI7Vl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />

Now, our goal is,

· Whenever the developer commits their code in GitHub, after every commit, it should reflect in the live web app.

· For that, we will use “GitScm polling”.

· Every time, a developer made a commit, a trigger will run automatically, which will rebuild the image and run a container on your behalf as a part of automation that will run the pipeline automatically.

25. Now, configure the project again, and add

Build Trigger: GitHub hook trigger for GitScm polling.

Description: GitHub webhook integration <br/>
<img src="https://i.imgur.com/p2dcgb4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />

26. We need to install the “Git Integration” plugin from Manage Jenkins, by following the path,

(Manage Jenkins > Manage Plugins > Git Integration). <br/>
<img src="https://i.imgur.com/Ta1Rcj5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
27. Now, Goto GitHub > Settings > SSH and GPG Keys > New SSH Key.

Add details as

Title: chetanrakhra@gmail.com

Key type: <public_key> <br/>
<img src="https://i.imgur.com/RrhyCzY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />

28. To get the Public key, open the “id_rsa.pub” file and copy the content. (Public Key) <br/>
<img src="https://i.imgur.com/jYEbm0K.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />

29. Now, we need to go to GitHub and create a new SSH and GPG Key.

GitHub > Repo “react-django-demo-app” > Settings > Webhooks.

30. Add the following details,

Payload URL: http://<public_ip_of_ec2>:8080/github-webhook/

Content-Type: application/json

Which event would you like to trigger this webhook?

o Just the push event.

Active: True

Click on “Add Webhook”. <br/>
<img src="https://i.imgur.com/eKGaAht.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />

31. Now, Save the configured project.

32. Do some changes in the code and push to GitHub, this will automatically run a pipeline, and the new code will be Live.
  <br/>
</p>
- <b>~Hassanat Hussain</b>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
