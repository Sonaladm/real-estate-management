pipeline {
    agent any

  
 
 
 // Building Docker images
        stage('Building image') {
            steps{
                script {
                    sh "docker build -t backend ./backend-fastify"
                    sh "docker build -t front ./frontend"   
                }
            }
        }
 


 //Creating container 
        stage('creating container for my-app') {
            steps{ 
                script {
                    sh "sudo docker rm -f ${IMAGE_REPO_NAME}-${BRANCH_NAME} || true"
                    sh "sudo docker images -a -q | xargs docker rmi -f || true"
                    sh " sudo docker run -d --name -p 4200:4200  front  "
                    sh " sudo docker run -d --name -p 8000:8000 backend  "
            }
        }
    }
}
}
