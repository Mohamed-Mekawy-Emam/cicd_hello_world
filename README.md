# hello-cicd
- Provision and configure ec2_instance on #aws using #Terrafrom as #jenkins agent
- Create #jenkins pipeline listens on #GitHub repo
- Dockerize simple Hello_world app using #Docker

# Local-Build
#### To build a docker image from the application

- docker build -t mmekawyhello:1.0 . 

- docker run -d -p 80:80 --name hello mmekawyhello:1.0

The dot "." at the end of the command denotes location of the Dockerfile.

Access you nodejs application UI from browser

    http://localhost:80

# Pre-requisites:

1. Jenkins master and Jenkins Slave is up and running
2. Docker installed on Jenkins Master and Slave instance.
3. Git installed on Jenkins Master and Slave instances.
4. Docker and Docker pipelines plug-in are installed on Jenkins Master.
5. Repo created in ECR in us-east-2 region.
6. Make sure port 80 is opened up in security group rules on Jenkins Master and slave. 
7. Create an IAM role with AmazonEC2ContainerRegistryFullAccess policy, attach to Jenkins Master and Slave EC2 instance
8. Make sure AWS cli is installed in Jenkins instance.

# Cloud-AWS-Build

Step 1: Provision Jenkins-Master

Jenkins-master

https://github.com/Mohamed-Mekawy-Emam/DevOps-Demos-Jenkins/tree/master/setup-jenkins

Step 2: Provision Jenkins-slave (Agent)

dev_server (Jenkins-Slave in our case)

Step 3: Configure Jenkins-Master to build through Jenkins-Slave

https://github.com/Mohamed-Mekawy-Emam/DevOps-Demos-Jenkins/tree/master/setup-jenkins-slave

1. Manage jenkins > Manage Nodes and Clouds > New Node

- Name = agent 
- Description = agent
- Number of executers = 1
- Remote root directory = /home/ubuntu/jenkins_home
- Labels = agent
- Launch method = Launch agent via SSH
- Host = <Jenkins_agent_public_ip  provisioned by Terraform>
- Credentials = <Add ubuntu(agent)>

2. Manage jenkins > Manage Nodes and Clouds > agent > Launch agent

- Waite until agent provisioned and active on AWS then you can see message "Agent successfully connected and online"

Step 4: Build pipeline from Jenkins-Master UI on Jenkins-Slave

pipeline "CICD_Hello_World" will be triggered automatically after pushing changes on repo and build and run container on Jenkins-slave

Step 5: access the application from browser

    http://Jenkins_agent_public_ip:80

