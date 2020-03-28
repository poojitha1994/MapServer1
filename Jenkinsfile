pipeline {
   agent any
  
   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
            sh 'whoami'
            sh 'cd /var/lib/jenkins/workspace/Mapserverdocker'
            sh 'ls /var/lib/jenkins/workspace/Mapserverdocker' 
            sh 'docker build -t mapserver1:1.0 . -f /var/lib/jenkins/workspace/Mapserverdocker/Dockerfile'
            sh 'docker-compose build'
            sh 'docker-compose up'
         }
      }
   }
}
