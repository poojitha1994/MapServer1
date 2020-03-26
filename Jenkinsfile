pipeline {
   agent any
  
   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
            sh 'whoami'
            sh 'cd /var/lib/jenkins/workspace/Test'
            sh 'ls /var/lib/jenkins/workspace/Test' 
            sh 'docker build -t mapserver1:1.0 . -f /var/lib/jenkins/workspace/Test'
            sh 'docker-compose build'
            sh 'docker-compose up'
         }
      }
   }
}
