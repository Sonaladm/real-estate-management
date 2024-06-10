pipeline{
    agent any
    
    stages{
        stage("logging in into ecr"){
            steps{
                
                  sh "aws ecr get-login-password --region ap-northeast-3 | docker login --username AWS --password-stdin 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com"
                
            }
        }
        stage("build the image"){
            steps{
            sh "docker build -t 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myecr:frontend ./frontend"
            sh "docker build -t 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myec:backend ./backend-fastify"
                
            }
            
        }
        stage("pusing to ecr"){
            steps{
            sh "docker push 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myecr:frontend"
            sh "docker push 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myecr:backend"
                
            }
            
        }
        stage("creating container"){
            steps{
            sh "docker run -d -p 4200:4200 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myecr:frontend"
            sh "docker run -d -p 8000:8000 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myecr:backend"
                
            }
        }
    }
        
    }
    
