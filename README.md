# Jenkins-Docker-Poc

# Usage

This will store the workspace in /var/jenkins_home. All Jenkins data lives in there - including plugins and configuration. You will probably want to make that an explicit volume so you can manage it and attach to another container for upgrades :

docker run -p 8080:8080 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts

this will automatically create a 'jenkins_home' docker volume on the host machine, that will survive the container stop/restart/deletion.

# Jenkins pipeline 

  - Created a pipeline using 'pipeline as Code'. Pipeline contain build, upload and deploy stages.
  - In build stage, created the docker image.
  - In upload stage, uploaded the image in a registry like Docker Hub with a different version label/tag. 
  - in deploy, deployed the container using latest code.
  - The pipeline runs when there are changes pushed to the Git repo.
  
# Node js application

created Dockerfile in docker-jenkins-poc/nodejs-demo/Dockerfile.
this app listens on port 3000, but the container should launch on port 80
