# Jenkins-Zero-To-Hero

Are you looking forward to learn Jenkins right from Zero(installation) to Hero(Build end to end pipelines)? then you are at the right place. 

## Installation on EC2 Instance

YouTube Video ->
https://www.youtube.com/watch?v=zZfhAXfBvVA&list=RDCMUCnnQ3ybuyFdzvgv2Ky5jnAA&index=1


![Screenshot 2023-02-01 at 5 46 14 PM](https://user-images.githubusercontent.com/43399466/216040281-6c8b89c3-8c22-4620-ad1c-8edd78eb31ae.png)

Install Jenkins, configure Docker as agent, set up cicd, deploy applications to k8s and much more.

## AWS EC2 Instance

- Go to AWS Console
- Instances(running)
- Launch instances

<img width="994" alt="Screenshot 2023-02-01 at 12 37 45 PM" src="https://user-images.githubusercontent.com/43399466/215974891-196abfe9-ace0-407b-abd2-adcffe218e3f.png">

### Install Jenkins.

Pre-Requisites:
 - Java (JDK)
### Run the below commands to install Jenkins and java if you are on a ubuntu or debian machine
```
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt install fontconfig openjdk-21-jre
sudo apt-get install jenkins

```
### Run the below commands to install Jenkins and java if you are on a redhat or fedora machine
```
sudo yum update
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io-2023.key
 sudo dnf upgrade
# Add required dependencies for the jenkins package
sudo dnf install fontconfig java-21-openjdk 
```

### If you are on amazon linux machine, use the following command to install java
```
 sudo amazon-linux-extras enable corretto11
 sudo yum install -y java-21-amazon-corretto
```
### Verify Java is Installed, make sure the version of java should be latest and compatible with jenkins.
```
java -version
```

Now, you can proceed with installing Jenkins

```
sudo dnf install jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```
### Check if the jenkins is running on port 8080 or anything other than jenkins running on port 8080
```
sudo netstat -tulnp | grep 8080
```
### If there is some problem running the jenkins server, run the below commands
```
 sudo systemctl daemon-reload
 sudo systemctl start jenkins
```
### To check the logs for jenkins, run the following commands
 ```
 sudo cat /var/log/jenkins/jenkins.log
 sudo systemctl status jenkins
 ls /var/log/jenkins
 sudo systemctl status jenkins -l
```
   
### **Note: ** If you are on AWS By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

- EC2 > Instances > Click on <Instance-ID>
- In the bottom tabs -> Click on Security
- Security groups
- Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed `All traffic`).

<img width="1187" alt="Screenshot 2023-02-01 at 12 42 01 PM" src="https://user-images.githubusercontent.com/43399466/215975712-2fc569cb-9d76-49b4-9345-d8b62187aa22.png">
```

### If you are on vmware or virtual machine, Jenkins will not be accessible to the external world due to the firewall restrictions of the port by the ubuntu os. Allow port 8080 in the firewall as show below.
```
sudo ufw allow 8080
sudo ufw reload
```
### Also check the network connection is selected to bridged connection which you want to access the jenkins server from any browser other than the host
### Also choose 

![image](https://github.com/user-attachments/assets/4a443ce5-dd62-4bf8-9744-81f05e708518)
### Also go to virtual network editor change settings. 
![image](https://github.com/user-attachments/assets/36b0daac-1547-4e7c-a6ac-31d8a963d161)
### Go to automatic settings and select the wireless or wifi adapter you are connected to and uncheck all other options
![image](https://github.com/user-attachments/assets/20092713-896b-45e9-b52e-4eb3ed895cc1)

### To see jenkins is running on the specific instance using port 8080:
```
ps -ef | grep jenkins
```
### Login to Jenkins using the below URL:

- http://<<"ec2-instance-public-ip-address">>:8080    [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]
- or http://<<"vm-ip-address">>:8080 [You can get the vm-ip-address bu using command]
- ```
  ip a | grep inet
  ```
- Note: If you are not interested in allowing `All Traffic` to your EC2 instance
      1. Delete the inbound traffic rule for your instance
      2. Edit the inbound traffic rule to only allow custom TCP port `8080`
  
After you login to Jenkins, 
      - Run the command to copy the Jenkins Admin Password - `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
      - Enter the Administrator password
      
<img width="1291" alt="Screenshot 2023-02-01 at 10 56 25 AM" src="https://user-images.githubusercontent.com/43399466/215959008-3ebca431-1f14-4d81-9f12-6bb232bfbee3.png">

### Click on Install suggested plugins

<img width="1291" alt="Screenshot 2023-02-01 at 10 58 40 AM" src="https://user-images.githubusercontent.com/43399466/215959294-047eadef-7e64-4795-bd3b-b1efb0375988.png">

Wait for the Jenkins to Install suggested plugins

<img width="1291" alt="Screenshot 2023-02-01 at 10 59 31 AM" src="https://user-images.githubusercontent.com/43399466/215959398-344b5721-28ec-47a5-8908-b698e435608d.png">

Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]

<img width="990" alt="Screenshot 2023-02-01 at 11 02 09 AM" src="https://user-images.githubusercontent.com/43399466/215959757-403246c8-e739-4103-9265-6bdab418013e.png">

Jenkins Installation is Successful. You can now starting using the Jenkins 

<img width="990" alt="Screenshot 2023-02-01 at 11 14 13 AM" src="https://user-images.githubusercontent.com/43399466/215961440-3f13f82b-61a2-4117-88bc-0da265a67fa7.png">

### Install the Docker Pipeline plugin in Jenkins:

   - Log in to Jenkins.
   - Go to Manage Jenkins > Manage Plugins.
   - In the Available tab, search for "Docker Pipeline".
   - Select the plugin and click the Install button.
   - Restart Jenkins after the plugin is installed.
   
<img width="1392" alt="Screenshot 2023-02-01 at 12 17 02 PM" src="https://user-images.githubusercontent.com/43399466/215973898-7c366525-15db-4876-bd71-49522ecb267d.png">

Wait for the Jenkins to be restarted.

### Git Installation on server
If you want to use code from github, makesure you have git installed on system
```
sudo apt install git
```
### Review of the jenkins architecture
- In the left side of the diagram, there is jenkins master, where the jenkins is right now installed.
- So this ec2 instance or ubuntu vm that we are using can be considered as jenkins master.
- What usually happens in an organization, let's say we are working for amazon.com. So there people create ec2 instance on jenkins master.
- There are multiple developers and multiple project teams. So jenkins gets a lot of load to offload these things.
- You should only use jenkins master only fot the scheduling purpose because all of the things cannot be run in a single jenkins master.
- If everything runs on a single jenkins master, then it will have conflicting packages such as one team requires java version 7 and another team requires java version 8. Someone request python2 and someone request python3.
-  It is technically not possible to have run everything on the jenkins master not good for the purpose of load and dependency conflicts.
-  So what people do is they create jenkins master and they create jenkins worker nodes, like worker node 1 should be used by applications 1 to 10. worker node 2 or 3 should be used by a specific development team.
-  With the advancement of kubernetes microservices architecture, the problem is that you have different types of application.
-  Only if your applications are light in weight then this container approach will work. If they are heavy applications like database then thos container approach might not work. We have to configure worker nodes.
  
![image](https://github.com/user-attachments/assets/520b5c02-8588-4df9-bdd4-53b4b60e4d18)

### Docker Slave Configuration

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
```
 
### Grant Jenkins user and Ubuntu user permission to docker deamon.

```
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```

Once you are done with the above steps, it is better to restart Jenkins.

```
http://<ec2-instance-public-ip>:8080/restart
```

The docker agent configuration is now successful.

![image](https://github.com/user-attachments/assets/f67f93fd-00d1-421e-8b80-b78106045103)


![image](https://github.com/user-attachments/assets/d603492c-da42-4d03-9e00-f42bf150aa35)

![image](https://github.com/user-attachments/assets/bf96ed62-2ab5-4917-affc-86d7e5290c6f)

### Your Jenkins build is failing due to low temporary space (/tmp), which has only 470.27 MB available. To increase it to 2 GB, follow these steps:
### Check Current /tmp Usage
```
df -h /tmp
```
This will show the total, used, and available space in /tmp
### Identify If /tmp is a Separate Partition
```
mount | grep /tmp
```
- If /tmp is on a separate partition, you need to resize it.
- If /tmp is using root (/) space, clearing files should help.
- Free Up Space in /tmp
### Delete unnecessary files:
```
sudo rm -rf /tmp/*
```
### Restart jenkins
```
sudo systemctl restart jenkins
```
### Check again
```
df -h /tmp
```
- Temporarily Increase /tmp Size (For Current Session)
### If /tmp is mounted using tmpfs, remount it with more space:
```
sudo mount -o remount,size=2G /tmp
```
### Verify:
```
df -h /tmp
```
- Permanently Increase /tmp Size (Persistent After Reboot)
### Edit /etc/fstab:
```
sudo nano /etc/fstab
```
### Find the line with /tmp and change it to:
```
tmpfs   /tmp   tmpfs   defaults,size=2G   0  0
```
### Save and exit, then reboot:
```
sudo reboot
```
### If /tmp is a Separate Partition (LVM)
```
sudo lvextend -L+2G /dev/your-tmp-lv
sudo resize2fs /dev/your-tmp-lv
```
### Check the space:
```
df -h /tmp
```
### Restart Jenkins
```
sudo systemctl restart jenkins
```

### If your Jenkins job is stuck waiting for an executor, which means no worker node is available to run the build. This can happen due to the following reasons:
### Check Number of Executors
- Go to Jenkins Dashboard → Manage Jenkins → Nodes and Clouds → Built-In Node
- Check # of Executors (should be at least 1).
- If it's 0, increase it to 1 and save.
### Check if Jenkins is Running as a Slave (Agent Mode)
- If you are using Jenkins agents, check whether they are connected and online.
- Go to Jenkins Dashboard → Manage Jenkins → Nodes and Clouds
- If all nodes are offline, restart them or reconfigure them.
### Restart Jenkins
Sometimes, a restart fixes the problem:
```
sudo systemctl restart jenkins
```
### Check Disk Space
Your /tmp partition was low on space earlier. If Jenkins is trying to use /tmp, it might be stuck:
```
df -h
```
### If /tmp is full, try:
```
sudo rm -rf /tmp/*
```
### Check jenkins logs:
```
sudo journalctl -u jenkins --no-pager | tail -50
```
### To check the tmp space is less, you can also see on your terminal using this command:
```
df -h /tmp
```

### To diagnose jenkins, you can also go to the foloowing path on jenkins dashboard.
- Manage Jenkins → System Information: Check memory, thread count, heap usage.
- Manage Jenkins → Load Statistics: Shows queue and executor usage over time.
- Thread Dump: Can show what Jenkins is “stuck” on (Manage Jenkins → Thread Dump).
- Also check your jenkins and java version is not outdated.
  
### If you lost the jenkins password, you can temporary login to jenkins server by
```
sudo systemctl stop jenkins
```
- Edit Jenkins config (in /var/lib/jenkins/config.xml or wherever your Jenkins home is):
```
<useSecurity>true</useSecurity>
```
- Change it to:
```
<useSecurity>false</useSecurity>
```
- Restart Jenkins
```
sudo systemctl restart jenkins
```
### Using Groovy Script (for scripting or automation)
If you’re automating Jenkins setup (e.g., in Docker or CI/CD), you can use a Groovy script from the Jenkins script console:

Go to:

Manage Jenkins → Script Console
paste this
```
import jenkins.model.*
import hudson.security.*

def instance = Jenkins.getInstance()
def hudsonRealm = new HudsonPrivateSecurityRealm(false)

hudsonRealm.createAccount("newuser", "password123")
instance.setSecurityRealm(hudsonRealm)
instance.save()

```
This creates a user newuser with password password123.
### After creating user, you don't want to automatically login into jenkins server so, in file /var/lib/jenkins, 
- REPLACE:
```
  <authorizationStrategy class="hudson.security.AuthorizationStrategy$Unsecured"/>
  <securityRealm class="hudson.security.SecurityRealm$None"/>
```
- WITH:
```
<securityRealm class="hudson.security.HudsonPrivateSecurityRealm">
  <disableSignup>true</disableSignup>
  <enableCaptcha>false</enableCaptcha>
</securityRealm>

<authorizationStrategy class="hudson.security.FullControlOnceLoggedInAuthorizationStrategy">
  <denyAnonymousReadAccess>true</denyAnonymousReadAccess>
</authorizationStrategy>

```
- Then Restart Jenkins:
```
sudo systemctl restart jenkins

```

