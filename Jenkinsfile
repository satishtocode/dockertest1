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
	        sh 'docker -H tcp://10.1.1.200:2375 stop app1'
	        sh  'docker -H tcp://10.1.1.200:2375 run --rm -dit --name app1 --hostname app1 -p 8006:80 8074764785/pipelinetest:v1'
	        sh 'docker -H tcp://10.1.1.200:2375 run --rm -dit --name app2 --hostname app2 -p 8007:80 8074764785/pipelinetest:v1'
		sh 'docker -H tcp://10.1.1.200:2375 run --rm -dit --name app3 --hostname app3 -p 8008:80 8074764785/pipelinetest:v1'
		  }
		}

	    stage('Check Webapp Reachability') {
		  steps {
	        sh 'sleep 10s'
	        sh 'curl http://ec2-13-233-128-254.ap-south-1.compute.amazonaws.com:8006'
		  }
	    }
    }
}
