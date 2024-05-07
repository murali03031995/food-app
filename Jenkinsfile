pipeline {
    agent any
    
environment {
    dockerhub=credentials('dockerhub')
    JENKINS_HOME=/home/ubuntu
    }     
    stages {        
        stage('checkout') {
            steps {
                sh 'git clone https://github.com/murali03031995/food-app.git '
                echo 'code pulled '
            }   
            }
        
        stage('build image') {
            steps {
                sh 'docker build -t murali1108/food-app -f /var/lib/jenkins/workspace/Backend_Pipeline/food-app/Dockerfile .'
                echo 'food-app image is build '
            }
            }
        
        stage('Docker Login') { 
            steps {
                sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'
            }
          }
          
         stage('Docker Push') {  
            steps {
                sh 'docker push murali1108/food-app'
            }
          }
        
        stage('Removing old docker container') {
            steps {
                
                sh 'docker container rm  foodcont -f'
                }
              }
              
        stage('Running the docker container') {
            steps {
                sh 'docker run -d  --name foodcont -p 80:80 murali1108/food-app'
                }
              } 
              
        
    }
}



