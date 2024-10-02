@Library("shared") _
pipeline{
    agent {label "tharun" }
    
    stages{
        stage("hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("code"){
           steps{
               echo"cloning the code"
               script{
                   clone("https://github.com/Iam-Tej23/django-notes-app","main")
               }
            } 
            
        }
        stage("build"){
          steps{
              echo"building the code"
              sh "docker build -t notes-app:latest ."
            }  
        }
        stage("pushing to docker Hub"){
           steps{
                echo"Pushing the image to dockerHub"
                withCredentials([usernamePassword(credentialsId:"dockerhubcred",passwordVariable:"DOCKER_PASS",usernameVariable:"DOCKER_USER")]){
                sh "docker login -u ${env.DOCKER_USER} -p ${env.DOCKER_PASS}"
                sh "docker image tag notes-app:latest ${env.DOCKER_USER}/notes-app:latest"
                sh "docker push 996tharuntej/notes-app:latest"
                }
            } 
            
        }
        stage("Deploy"){
            steps{
                echo"building the code"
                sh "docker compose down && docker compose up -d"
            }
            
        }
    }
}
