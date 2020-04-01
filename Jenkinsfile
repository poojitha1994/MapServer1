pipeline {
   
  agent any
   stages{
      stage('Create Image') {
         steps{
         
            echo 'Hello World'
            sh 'whoami'
            sh 'cd /var/lib/jenkins/workspace/Mapserverdocker'
            sh 'ls /var/lib/jenkins/workspace/Mapserverdocker' 
            sh 'docker build -t openstreetmap:latest . -f /var/lib/jenkins/workspace/Mapserverdocker/Dockerfile'
            sh 'docker-compose build'
      }
      }
   stage('Push Image to AWS ECR'){
      steps{
         script{
           docker.withRegistry('https://505096120716.dkr.ecr.ap-southeast-1.amazonaws.com', 'ecr:ap-southeast-1:ecr-credentials') {
                  // sh "docker push 505096120716.dkr.ecr.ap-southeast-1.amazonaws.com/mapserver:latest"
              //docker.image('openstreetmap:latest').push()
              sh "docker tag openstreetmap:latest 505096120716.dkr.ecr.ap-southeast-1.amazonaws.com/mapserver:latest"
              sh "docker push 505096120716.dkr.ecr.ap-southeast-1.amazonaws.com/mapserver:latest"
                         }
         
      }

      }
      
   }
   }
       post {
        success {
            emailext (
                to: 'poojithars34@gmail.com',
                subject: "SUCCESS",
                body: "SUCCESS!"
            )
        }
        failure {
			emailext (
                to: 'poojithars34@gmail.com',
                subject: "FAILURE",
                body: "FAILURE!"
            )
        }
    }
}
