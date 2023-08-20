pipeline {
  agent any
  stages {

    stage('Docker build and push') {
      steps {
		sh '''
		 whoami
		 aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 855991486920.dkr.ecr.ap-south-1.amazonaws.com
		 docker build -t dotnet-application .	
		 docker tag dotnet-application:latest 855991486920.dkr.ecr.ap-south-1.amazonaws.com/dotnet-application:${BUILD_NUMBER}
		 docker push 855991486920.dkr.ecr.ap-south-1.amazonaws.com/dotnet-application:${BUILD_NUMBER}
		  '''
	     }	         
	   }

    stage('Deploy docker'){
      steps {
		sh '''
			  ssh -i /var/lib/jenkins/application.pem -o StrictHostKeyChecking=no ubuntu@ec2-13-232-140-120.ap-south-1.compute.amazonaws.com 'bash -s' < ./deploy.sh \${BUILD_NUMBER}
			  '''	 
		    
      		}
		}		    

}

 }
