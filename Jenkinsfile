pipeline {
   agent any
  
   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
            sh 'sudo -tt /usr/bin/rsync'
            sh 'cd /var/lib/jenkins/workspace/Test'
            sh 'ls /var/lib/jenkins/workspace/Test' 
            sh 'sudo -n docker build -t mapserver1:1.0 .'
            sh 'sudo -n docker-compose build'
            sh 'sudo -n docker-compose up'
         }
      }
   }
}
