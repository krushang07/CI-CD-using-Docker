pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/krushang07/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Build Docker Image'){
     sh 'docker build -t krushang007/app .'
   }
    stage('Push Docker Image'){
   withCredentials([string(credentialsId: 'krushang007', variable: 'dockerhubpwd')]) {
     sh "docker login -u krushang007 -p ${dockerhubpwd}"
     }
     sh 'docker push krushang007/app'
   }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 krushang007/app"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://ubuntu@172.31.20.66 run -d -p 8003:8080 krushang007/app"
 
            }
        }
    }
	}
    
