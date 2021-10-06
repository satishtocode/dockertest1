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
	        sh 'docker service create --name test -p 8007:80 --replicas 4 8074764785/pipelinetest:v1'
	        
		  }
		}

	    stage('Check Webapp Reachability') {
		  steps {
	        sh 'sleep 10s'
	        sh 'curl http://www.antraders.live'
		  }
	    }
    }
}
