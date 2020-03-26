pipeline {
   agent any
  
   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
            sh 'cd /var/lib/jenkins/workspace/Test'
            sh 'ls /var/lib/jenkins/workspace/Test' 
            sh 'sudo docker build -t mapserver1:1.0 .'
            sh 'sudo docker-compose build'
            sh 'sudo docker-compose up'
         }
      }
   }
}
