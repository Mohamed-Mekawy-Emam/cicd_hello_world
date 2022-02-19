pipeline {
    agent any
    environment {
        // replace acc_id , us-east-2 , your_ecr_repo with your own data accross this Jenkinsfile
        registry = "acct_id.dkr.ecr.us-east-2.amazonaws.com/your_ecr_repo"
    }
   
    stages {
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/Mohamed-Mekawy-Emam/cicd_hello_world']]])     
            }
        }
  
    // Building Docker images
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }
	
    // Uploading Docker images into AWS ECR
    stage('Pushing to ECR') {
      steps{  
         script {
                sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin acct_id.dkr.ecr.us-east-2.amazonaws.com'
                sh 'docker push acct_id.dkr.ecr.us-east-2.amazonaws.com/your_ecr_repo:latest'
         }
        }
      }

    // Stopping Docker containers for cleaner Docker run
    stage('stop previous containers') {
      steps {
            sh 'docker ps -f name=hello -q | xargs --no-run-if-empty docker container stop'
            sh 'docker container ls -a -fname=hello -q | xargs -r docker container rm'
         }
       }
      
    stage('Docker Run') {
     steps{
         script {
                sh 'docker run -d -p 80:80 --rm --name hello acct_id.dkr.ecr.us-east-2.amazonaws.com/your_ecr_repo:latest'
            }
      }
    }
    }
}