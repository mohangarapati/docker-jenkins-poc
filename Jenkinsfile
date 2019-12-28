pipeline {
    agent any

    stages {
	    stage('Clone sources') {
            git : 'https://github.com/mohangarapati/docker-jenkins-poc.git'
         }

        stage('Build image') {
            steps {
               	sh 'echo Starting to build docker image'
		        sh 'cd $JENKINS_HOME/docker-jenkins-poc/nodejs-demo'
	    stage('Docker Build') {
     	    steps {
        	    sh 'docker build -t mohangarapatidoc/docker-jenkins-poc:latest .'
             }
            }
	    stage('Docker upload') {
      	     steps {
        	    withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          	    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          	    sh 'docker push mohangarapatidoc/docker-jenkins-poc:latest'
	            }
     	   }
        stage('Docker Deploy') {
            steps {
                sh 'docker run -t -p 80:3000 -d mohangarapatidoc/docker-jenkins-poc:latest'
            }
            }

   	     }
       }
     }
   }
}	
