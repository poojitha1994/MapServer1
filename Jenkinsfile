pipeline {
   agent any
  
   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
            sh 'cd /var/lib/jenkins/workspace/Mapserver1'
            sh 'ls /var/lib/jenkins/workspace/Mapserver1' 
            sh 'docker build -t mapserver1:1.0 .'
            sh 'docker-compose build'
            sh 'docker-compose up'
         }
      }
   }
}
