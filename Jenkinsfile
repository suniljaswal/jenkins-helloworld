pipeline {
    agent any
    
    stages {
        stage('Fetch dependencies') {
        /* This stage pulls the latest image from
           Dockerhub */
            steps {
                sh 'sudo docker pull karthequian/helloworld:latest'
          }
        }
        stage('Build docker image') {
        /* This stage builds the actual image; synonymous to
           docker build on the command line */
            steps {
            sh "sudo docker build . -t customapp:1"
            }    
        }
        stage('Test image') {
         /* This stage runs unit tests on the image; we are
            just running dummy tests here */
            steps {
                sh 'echo "Tests successful"'
          }
        }
        stage('Push image to OCIR') {
         /* Final stage of build; Push the 
            docker image to our OCI private Registry*/
        steps {
            sh "sudo docker login -u 'bmsondaagodo/nothingelse007@gmail.com' -p 'z<){[[Y41Ffxwo-D;kuy' 'ap-mumbai-1.ocir.io'"
            sh "sudo docker tag customapp:1 ap-mumbai-1.ocir.io/bmsondaagodo/customapp:custom"
            sh 'sudo docker push ap-mumbai-1.ocir.io/bmsondaagodo/customapp:custom'
            
           }
         } 
         stage('Deploy to OKE') {
         /* Deploy the image to OKE*/

        steps {
            /*sh "'sudo cp /var/lib/jenkins/workspace/deploy.sh /var/lib/jenkins/workspace/jenkins-oci_master'"*/
            sh 'sh ../../hello-deploy.sh'
           }
         }     
    }
}
