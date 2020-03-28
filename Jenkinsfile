pipeline {
   agent any
  
   stages {
      stage('Stage1') {
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
       stage('Stage2') {
         steps {
                  docker.withRegistry('https://505096120716.dkr.ecr.ap-southeast-1.amazonaws.com/mapserver', 'ecr:Singapore:ecr-credentials') {
                  docker.image(' mapserver1').push('1.0')
         }
      }
   }
}
