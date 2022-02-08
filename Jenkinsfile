pipeline {
  agent {label 'agent'}
stages {
          stage('start') {
            steps {
              script {
                    sh 'docker kill $(docker ps -q)'
                    sh 'docker build -t mmekawy/hello:lts .'
                    sh 'docker run -d -p 80:80 mmekawy/hello:lts'
              
            }
            }
          }
}
}
