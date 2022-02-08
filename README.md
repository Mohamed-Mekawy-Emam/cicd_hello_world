# hello-cicd
- Provision and configure ec2_instance on #aws using #Terrafrom as #jenkins agent
- Create #jenkins pipeline listens on #GitHub repo
- Dockerize simple Hello_world app using #Docker

# Local-Build
#### To build a docker image from the application
docker build -t mmekawy/hello:lts . 
docker run -d -p 80:80 mmekawy/hello:lts

The dot "." at the end of the command denotes location of the Dockerfile.

Access you nodejs application UI from browser

    http://localhost:80

# Cloud-AWS-Build

Step 1: Provision Jenkins-Master
Jenkins-master

Step 2: Provision Jenkins-slave (Agent)
dev_server

Step 3: Configure Jenkins-Master to build through Jenkins-Slave
1. Manage jenkins > Manage Nodes and Clouds > New Node
Name = agent 
Description = agent
Number of executers = 1
Remote root directory = /home/ubuntu/jenkins_home
Labels = agent
Launch method = Launch agent via SSH
Host = <Jenkins_agent_public_ip  provisioned by Terraform>
Credentials = <Add ubuntu(agent)>

2. Manage jenkins > Manage Nodes and Clouds > agent > Launch agent
Waite until agent provisioned and active on AWS then you can see message "Agent successfully connected and online"

Step 4: Build pipeline from Jenkins-Master UI on Jenkins-Slave
pipeline "CICD_Hello_World" will be triggered automatically after pushing changes on repo and build and run container on Jenkins-slave

Step 5: access the application from browser
    http://Jenkins_agent_public_ip:80

