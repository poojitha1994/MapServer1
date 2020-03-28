node {
    def app
  
  
      stage('Stage1') {
         
            echo 'Hello World'
            sh 'whoami'
            sh 'cd /var/lib/jenkins/workspace/Mapserverdocker'
            sh 'ls /var/lib/jenkins/workspace/Mapserverdocker' 
            sh 'docker build -t mapserver1:latest . -f /var/lib/jenkins/workspace/Mapserverdocker/Dockerfile'
            sh 'docker-compose build'
      }
   stage('Stage 2'){
           docker.withRegistry('https://505096120716.dkr.ecr.ap-southeast-1.amazonaws.com', 'ecr:ap-southeast-1:ecr-credentials') {
                   sh "docker push 505096120716.dkr.ecr.ap-southeast-1.amazonaws.com/mapserver:latest"
         
         
      }
   }
}
