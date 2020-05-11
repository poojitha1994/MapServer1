pipeline {
   
  agent any
   stages{
      stage('Build') {
         steps{
         
            echo 'Building Docker image for mapserver'
            sh 'whoami'
            sh 'chmod -R 777 /var/lib/jenkins/workspace/OSM_MapServer'
            sh 'cd /var/lib/jenkins/workspace/OSM_MapServer'
            sh 'ls /var/lib/jenkins/workspace/OSM_MapServer' 
            sh 'docker build -t openstreetmap:${BUILD_NUMBER} . -f /var/lib/jenkins/workspace/OSM_MapServer/Dockerfile'
           
      }
      }
  /* stage('Push Image to AWS ECR'){
      steps{
         script{
           docker.withRegistry('https://505096120716.dkr.ecr.ap-southeast-1.amazonaws.com', 'ecr:ap-southeast-1:ecr-credentials') {
                  // sh "docker push 505096120716.dkr.ecr.ap-southeast-1.amazonaws.com/mapserver:latest"
              //docker.image('openstreetmap:latest').push()
              sh "docker tag openstreetmap:${BUILD_NUMBER} 505096120716.dkr.ecr.ap-southeast-1.amazonaws.com/mapserver:${BUILD_NUMBER}"
              sh "docker push 505096120716.dkr.ecr.ap-southeast-1.amazonaws.com/mapserver:${BUILD_NUMBER}"
                         }
         
      }

      }
      
   }*/
      stage('Push to ECR'){
         steps{
            echo 'push image to ecr'
          //sh 'docker login https://505096120716.dkr.ecr.ap-southeast-1.amazonaws.com'
          
            sh '''echo $(aws ecr get-authorization-token --region ap-southeast-1 --output text --query 'authorizationData[].authorizationToken' | base64 -d | cut -d: -f2) | docker login -u AWS https://505096120716.dkr.ecr.ap-southeast-1.amazonaws.com --password-stdin''' 
           sh  'docker tag openstreetmap:${BUILD_NUMBER} 505096120716.dkr.ecr.ap-southeast-1.amazonaws.com/mapserver:${BUILD_NUMBER}'
           sh ' docker push 505096120716.dkr.ecr.ap-southeast-1.amazonaws.com/mapserver:${BUILD_NUMBER}'
         }
      }
  stage('Scan Docker images'){
         steps{
        
            /*sh 'aws ecr start-image-scan \
            --repository-name valhalla \
            --image-id imageTag=${BUILD_NUMBER} \
            --region ap-southeast-1 --output json| tee ecr_start_scan_${BUILD_NUMBER}.txt' */
            //aws ecr get-login
          
            sh '''  aws ecr start-image-scan --registry-id 505096120716 \
                           --repository-name mapserver\
                           --image-id imageTag=${BUILD_NUMBER} '''
            sleep(60)
       
           /* sh 'aws ecr describe-image-scan-findings \
            --repository-name valhalla \
            --image-id imageTag=${BUILD_NUMBER} \
            --region ap-southeast-1 | tee ecr_scanResult_${BUILD_NUMBER}.txt'*/
            //sh 'aws ecr put-image-scanning-configuration --repository-name valhalla--image-scanning-configuration scanOnPush=true --region ap-southeast-1'
     sh ''' aws ecr describe-image-scan-findings --registry-id 505096120716 \
                                       --repository-name mapserver\
                                       --image-id imageTag=${BUILD_NUMBER}  --output json | tee Valhalla_ecr_scanResult_${BUILD_NUMBER}.txt'''
      // pull image form ecr command:  sudo docker pull 505096120716.dkr.ecr.ap-southeast-1.amazonaws.com/valhalla:latest

         }
      }
stage('Slack Notification'){
            steps{
                slackSend channel: 'U010CRSPF9R', message: 'From jenkins, Batch job completed'
            }
        }

   }
}
