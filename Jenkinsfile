pipeline {
    agent any
    stages { 

	    stage('Clone Repo') {
		  steps {
	        sh 'rm -rf dockertest1'
	                sh 'git clone https://github.com/satishtocode/dockertest1.git'
		  }		
	    }

	    stage('Build Docker Image') {
		  steps {
	        sh 'cd /var/lib/jenkins/workspace/pipeline2/dockertest1'
	        sh 'cp /var/lib/jenkins/workspace/pipeline2/dockertest1/* /var/lib/jenkins/workspace/pipeline2'
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
	        sh  'docker -H tcp://10.1.1.200:2375 run --rm -dit --name app1 --hostname app1 -p 8006:80 8074764785/pipelinetest:v1'
		  }
		}

	    stage('Check Webapp Reachability') {
		  steps {
            sh 'sleep 10s'
	        sh 'curl http://ec2-3-108-191-183.ap-south-1.compute.amazonaws.com:8006'
		  }
	    }
    }
}
