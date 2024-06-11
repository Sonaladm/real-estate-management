
pipeline{
    agent any
    stages{
        stage ("login to ecr"){
            steps {
               sh "aws ecr get-login-password --region ap-northeast-3 | docker login --username AWS --password-stdin 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com"
            }
        }
        stage ("build"){
            steps {
                sh "docker build -t 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/newecr:frontend ./frontend"
                sh "docker build -t 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/newecr:backend ./backend-fastify"
            }
        
        }
        stage ("push"){
            steps {
                sh "docker push 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/newecr:frontend" 
                sh "docker push 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/newecr:backend"
            }
            
        }
        stage ("deploy"){
            steps {
                sh "ssh ubuntu@13.208.184.73 /home/ubuntu/login.sh"
                sh "ssh ubuntu@13.208.184.73 docker run -d -p 4200:4200 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/newecr:frontend "
                sh "ssh ubuntu@13.208.184.73 docker run -d -p 8000:8000 682484440485.dkr.ecr.ap-northeast-3.amazonaws.com/newecr:backend "
            }
            
        }
    }
}
