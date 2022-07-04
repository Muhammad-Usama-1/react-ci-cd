pipeline {   
  agent any  
  environment {     
    DOCKERHUB_CREDENTIALS= credentials('docker-hub-credentials')     
  }    
  stages {         
    stage("Git Checkout"){           
      steps{                
	git credentialsId: 'github', url: 'https://github.com/Muhammad-Usama-1/react-ci-cd'                 
	echo 'Git Checkout Completed'            
      }        
    }
    stage('Build Docker Image') {         
      steps{                
	sh 'docker build -f Dockerfile.prod -t sample:prod .'           
        echo 'Build Image Completed'                
      }           
    }
    stage('Login to Docker Hub') {         
      steps{                            
	sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                 
	echo 'Login Completed'                
      }           
    }               
    stage('Push Image to Docker Hub') {         
      steps{                            
	sh 'docker push usama855/new:$BUILD_NUMBER'
        echo 'Push Image Completed'       
      }           
    }      
  } //stages 
  post{
    always {  
      sh 'docker logout'           
    }      
  }  
} //pipeline
