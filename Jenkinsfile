pipeline {
    agent any
    stages { 

	    stage('Clone Repo') {
	        sh 'rm -rf dockertest1'
	                sh 'git clone https://github.com/satishtocode/dockertest1.git'
	    }

	    stage('Build Docker Image') {
	        sh 'cd /var/lib/jenkins/workspace/pipeline2/dockertest1'
	        sh 'cp /var/lib/jenkins/workspace/pipeline2/dockertest1/* /var/lib/jenkins/workspace/pipeline2'
	        sh 'docker build -t 8074764785/pipelinetest:v1 .'
	    }

	    stage('Push Image to Docker Hub') {
	    sh  'docker push 8074764785/pipelinetest:v1'
        }

	    stage('Deploy to Docker Host') {
	    sh 'docker -H tcp://10.1.1.200:2375 stop webapp1'
	    sh  'docker -H tcp://10.1.1.200:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 8005:80 8074764785/pipelinetest:v1'
        }

	    stage('Check Webapp Reachability') {
        sh 'sleep 10s'
	    sh 'curl http://ec2-65-0-3-162.ap-south-1.compute.amazonaws.com:8005'
	    }
    }
}
