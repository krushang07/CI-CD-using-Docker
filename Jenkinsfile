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
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp krushang007/samplewebapp:latest'
                
               
          }
        }
     stage('Publish image to Docker Hub') {
          
            steps {
       withCredentials([string(credentialsId: 'krushang007', variable: 'dockerhubpwd')])  {
       sh "docker login -u krushang007 -p ${dockerhubpwd}"
          sh  'docker push krushang007/samplewebapp:latest'
        
        }
                  
          }
        }
        
        stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.95.188 run -d -p 8005:8080 krushang007/samplewebapp"
 
            }
        }

    
 }
}
