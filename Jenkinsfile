pipeline {
   agent any
   triggers {
    pollSCM '* * * * *'
    }
    stages {
      stage('Docker build') {
         steps {
            // Get some code from a GitHub repository
            //git 'https://github.com/mohangarapati/docker-jenkins-poc.git'
            
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'nodejs-demo']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'c76de21c-3533-47d8-bf8f-102f4a4fe2f8', url: 'https://github.com/mohangarapati/docker-jenkins-poc.git']]])
            sh "cd $WORKSPACE/nodejs-demo/nodejs-demo/ && ls"
            
            dir("$WORKSPACE/nodejs-demo/nodejs-demo/"){
                sh "pwd"
                sh "docker build -t mohangarapatidoc/docker-jenkins-poc:latest ."
            }
            
            sh "pwd; ls"

            // Run Maven on a Unix agent.
            //sh "docker build -t mohangarapatidoc/docker-jenkins-poc:latest ."

            // To run Maven on a Windows agent, use
            // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
      }
      stage('Docker upload') {
        steps {
            withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          	sh 'docker push mohangarapatidoc/docker-jenkins-poc:latest'
	            }
     	   }
      }
      stage('Docker deploy') {
            steps {
                sh 'docker run -t -p 80:3000 -d mohangarapatidoc/docker-jenkins-poc:latest'
            }
        }
    }  
}    
