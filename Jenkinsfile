pipeline {
  agent {label 'agent'}
stages {
          stage('start') {
            steps {
              script {
                    sh 'docker kill $(docker ps -q)'
                    sh 'docker build -t mmekawyhello:1.0 .'
                    sh 'docker run -d -p 80:80 mmekawyhello:1.0'
              
            }
            }
          }
}
}
