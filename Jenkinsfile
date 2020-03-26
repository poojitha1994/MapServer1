pipeline {
   agent any
  
   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
            sh 'sudo -tt /usr/bin/rsync'
            sh 'cd /var/lib/jenkins/workspace/Test'
            sh 'ls /var/lib/jenkins/workspace/Test' 
            sh 'docker build -t mapserver1:1.0 .'
            sh 'docker-compose build'
            sh 'docker-compose up'
         }
      }
   }
}
