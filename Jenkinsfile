pipeline{
    agent any
    
    stages{
        stage("logging in into ecr"){
            steps{
                
                  sh "aws ecr get-login-password --region ap-northeast-3 | docker login --username AWS --password-stdin 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com"
                  sh "docker images -a -q | xargs docker rmi -f || true"
            }
        }
        stage("build the image"){
            steps{
            sh "docker build -t frontendmyecr682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myecr:latest ./frontend"
            sh "docker build -t backendmyecr682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myecr:latest ./backend-fastify"
                
            }
            
        }
        stage("pusing to ecr"){
            steps{
            sh "docker push frontendmyecr682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myecr:latest"
            sh "docker push backendmyecr682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myecr:latest"
                
            }
            
        }
        stage("creating container"){
            steps{
            sh "docker run -d -p 4200:4200 frontendmyecr682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myecr:latest"
            sh "docker run -d -p 8000:8000 backendmyecr682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/myecr:latest"
                
            }
        }
    }
        
    }
    
