pipeline {
    agent any

    stages {
        stage('Cloning the code') {
            steps {
                echo 'Cloning the code'
                git url:"https://github.com/Iam-Tej23/django-notes-app",branch:"main"
            }
        }
          stage('Building the code') {
            steps {
                echo 'Build the code'
             
            }
        }
            stage('Pushing the code') {
            steps {
             echo"Pushing the image to dockerHub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"DOCKER_PASS",usernameVariable:"DOCKER_USER")]){
                sh "docker login -u ${env.DOCKER_USER} -p ${env.DOCKER_PASS}"
                sh "docker image tag app:latest ${env.DOCKER_USER}/app:latest"
                sh "docker push 996tharuntej/app:latest"
                }
            }
        }
            stage('Deploying the code') {
            steps {
                echo 'Deploying the Application'
                sh 'docker compose down'
                sh 'docker compose up -d'
                echo 'Deployment is successful'
            }
        } 
    }
}
