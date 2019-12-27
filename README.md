# jenkins-docker-poc
This repo contains a Node.js app, you need to get it running in a container
# Overview of this assignment
  - Use the instructions from developer below to create a working Dockerfile
  - once Dockerfile builds correctly, start container locally to make sure it works on http://localhost or your VM's public IP
  - then ensure image is named properly for your Docker Hub account with a new repo name
  - push to Docker Hub, then go to https://hub.docker.com and verify
  - then remove local image from cache
  - then start a new container from your Hub image, and watch how it auto downloads and runs
  - test again that it works at http://localhost
  - Install Jenkins using docker image, use bind mount to store JENKINS_HOME directory.
  - Create a pipeline using 'pipeline as Code'. Pipeline should contain build, upload and deploy stages.
  - In build stage, you create the docker image.
  - In upload stage, you upload the image in a registry like Docker Hub with a different version label/tag. 
  - in deploy, you start the container using latest code.
  - The pipeline must run when there are changes pushed to the Git repo.
# Instructions from the app developer
 - you should use the 'node' official image, with the alpine 6.x branch
 - this app listens on port 3000, but the container should launch on port 80
 -  so it will respond to http://localhost:80 on your computer
 - then it should use alpine package manager to install tini: 'apk add --update tini'
 - then it should create directory /usr/src/app for app files with 'mkdir -p /usr/src/app'
 - Node uses a "package manager", so it needs to copy in package.json file
 - then it needs to run 'npm install' to install dependencies from that file
 - to keep it clean and small, run 'npm cache clean --force' after above
 - then it needs to copy in all files from current directory
 - then it needs to start container with command '/sbin/tini -- node ./bin/www'
 - in the end you should be using FROM, RUN, WORKDIR, COPY, EXPOSE, and CMD commands

 Bonus: This is just meant to get you started with basic Dockerfile concepts and not focus too much on
 proper Node.js use in a container. **If you happen to be a Node.js Developer**, then 
 after you get through more of this course, youmay refer 'Node Docker Good Defaults' sample project on GitHub to change this Dockerfile for 
 better local development with more advanced topics
 https://github.com/BretFisher/node-docker-good-defaults
