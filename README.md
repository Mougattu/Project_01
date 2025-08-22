Project details---Deploying Tomcat Web App on AWS

I have deployed a Tomcat web app on AWS. The way I approached is to use an Amazon EC2 instance and install Tomcat there.

Steps to deploy Tomcat app on AWS EC2:

Step 1: Launch an AWS EC2 instance

Going to the AWS Management Console.

Opened EC2 Dashboard.

Clicked on Launch Instance.

Choosen an Amazon Linux AMI
Choosen an instance type (t3.micro eligible for free tier).

Configured instance details as below.

Instance name--Ec2user-mum-01 with a public IP.

storage (default).

Configured security group:

Allowed SSH (port 22) from IP.

Allowed HTTP (port 80) from anywhere (for web traffic).

Allowed Tomcat default port 8080 from anywhere (optional, for testing).

Reviewed and launched.

Downloaded the key pair (.ppk file) to connect the instance.

Step 2: Connected to EC2 instance using SSH with public ip and key pair.

Step 3: Installed Java and Tomcat on EC2

For Amazon Linux 2:

sudo yum update -y
sudo yum install java-1.8.0-openjdk -y   
java -version                            

# Downloaded Tomcat 9
cd /opt
sudo wget https://downloads.apache.org/tomcat/tomcat-9/v9.0.108/bin/apache-tomcat-9.0.108.tar.gz.asc ---(for downloading the tomcat)
sudo tar xvf apache-tomcat-9.0.108.tar.gz.asc (for extracting the tomcat files)
sudo mkdir tomcat9 (creating folder)
sudo mv apache-tomcat-9.0.108.tar.gz.asc tomcat9 (moving the tomcat file to tomcat9 folder)
sudo chmod -R 755 /opt/tomcat9 (giving required permission to folder to start tomcat)
sudo chmod +x /opt/tomcat9/bin/*.sh  (giving required permission to folder to start tomcat)
sudo chown -R ec2-user:ec2-user/opt/tomcat9  (giving required permission to folder to start tomcat)

Step 4 : Started Tomcat using below command

sudo /opt/tomcat9/bin/startup.sh

Step 5: Accessed app using below url

http://your-ec2-public-ip:8080/myapp
