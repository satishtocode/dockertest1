pipeline {
    agent any
    stages { 

	    stage('Clone Repo') {
		  steps {
	                sh 'git clone https://github.com/satishtocode/dockertest1.git'
		  }		
	    }

	    stage('Build Docker Image') {
		  steps {
	        sh 'cd /var/lib/jenkins/workspace/pipelinetest/dockertest1'
	        sh 'cp /var/lib/jenkins/workspace/pipelinetest/dockertest1/* /var/lib/jenkins/workspace/pipelinetest'
	        sh 'docker build -t 8074764785/pipelinetest:v1 .'
		  }
	    }

	    stage('Push Image to Docker Hub') {
		  steps {
	        sh  'docker push 8074764785/pipelinetest:v1'
		  }		
        }

	    stage('Deploy to Docker Host') {
		  steps {
	        sh 'docker -H tcp://10.1.1.181:2375 stop test'
	        sh 'docker -H tcp://10.1.1.181:2375 run --rm -dit --name test --hostname test -p 8007:80 8074764785/pipelinetest:v1'
	        
		  }
		}

	    stage('Check Webapp Reachability') {
		  steps {
	        sh 'sleep 10s'
	           sh 'curl http://ec2-13-233-89-241.ap-south-1.compute.amazonaws.com:8007'
		  }
	    }
    }
}
