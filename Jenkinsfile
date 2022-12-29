def qa_server_ip="";
def prod_server_ip="";
pipeline {
    agent{label 'debian'} // debian node is QA environment
    stages {
        stage('Clone QA env') {
            steps {
                git 'https://github.com/jhossmar/books_management_cicd.git'
            }            
        }
        stage('Docker images build'){
            steps{
                dir('client'){
                    sh "docker build -t frontend:1.0 ."

                }
                dir('server'){
                    sh 'docker build -t backend:1.0 .'
                }
                sh "docker images"
            }
        }
        stage('Deploy QA environment'){
            steps{
                git 'https://github.com/jhossmar/books_management_cicd.git'
                sh "docker compose up -d"
                sh "docker compose ps"
            }
        }
        stage('Save docker images'){
            steps{
                sh "docker save frontend:1.0 | gzip > frontend1.0.tar.gz"
                sh "docker save backend:1.0 | gzip > backend1.0.tar.gz"
                sh "ls -alth"
                stash includes: 'frontend1.0.tar.gz', name: 'frontend_image'
                stash includes: 'backend1.0.tar.gz', name: 'backend_image'
            }

        }
        stage ('Deploy PROD environment'){
            agent{label 'prod'}
            steps{
                git 'https://github.com/jhossmar/books_management_cicd.git'
                unstash 'backend_image'
                unstash 'frontend_image'
                sh "docker compose -f docker-compose-prod.yml down"
                sh "echo 'Y' | docker image prune -a "
                sh "docker load -i frontend1.0.tar.gz"
                sh "docker load -i backend1.0.tar.gz"
                sh "docker compose -f docker-compose-prod.yml up -d "
            }
        }
    }
}
