pipeline {
    agent any

    /* parameters {
        string(
            name: 'AWS_ACCOUNT_ID',
            description: 'Account ID of the AWS you want to build'
        ),
        string(
            name: 'AWS_DEFAULT_REGION',
            description: 'Name of the Region you want to build'
        ),
        string(
            name: 'BRANCH_NAME',
            description: 'Name of the branch you want to build'
        )

    }*/

    environment {
        AWS_ACCOUNT_ID="682484440485"
        AWS_DEFAULT_REGION="ap-northeast-3"
        BRANCH_NAME="main"
        IMAGE_REPO_NAME="myecr"
        REPOSITORY_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
    }
 
    stages {
 
        stage('Logging into AWS ECR') {
            steps {
                script {
                    sh "aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"
                    sh "docker images -a -q | xargs docker rmi -f || true"
                }
 
            }
        }
 
 
 // Building Docker images
        stage('Building image') {
            steps{
                script {
                    sh "docker build -t ${REPOSITORY_URI}:${BRANCH_NAME} ./backend-fastify"
                    sh "docker build -t front${REPOSITORY_URI}:${BRANCH_NAME} ./frontend"   
                }
            }
        }
 


 //Creating container 
        stage('creating container for my-app') {
            steps{ 
                script {
                    sh "  /home/ubuntu/login-ecr.sh"             
                    sh "sudo docker rm -f ${IMAGE_REPO_NAME}-${BRANCH_NAME} || true"
                    sh "sudo docker images -a -q | xargs docker rmi -f || true"
                    sh " sudo docker network create sonal"
                    sh " sudo docker run -itd --name ${IMAGE_REPO_NAME}-${BRANCH_NAME} --network sonal -p 4200:4200 --restart always ${REPOSITORY_URI}:${BRANCH_NAME}"
                    sh " sudo docker run -itd --name front${IMAGE_REPO_NAME}-${BRANCH_NAME} --network sonal -p 8000:8000 --restart always front${REPOSITORY_URI}:${BRANCH_NAME}"
                    
                }
            }
        }
    }
}
