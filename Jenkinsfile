pipeline {
    agent any

    stages {

        stage('Build docker image') {
            steps {
                sh 'docker build -t danwhite123/nginx-image:latest -f Dockerfile_nginx .'
            }
        }

        stage('Push docker image to DockerHub') {
            steps {
                withDockerRegistry(credentialsId: 'docker-hub-cred', url: 'https://index.docker.io/v1/') {
                    sh '''
                        docker push danwhite123/nginx-image:latest
                    '''
                }
            }
        }

        stage('Delete docker image locally') {
            steps{
                sh 'docker rmi -f danwhite123/nginx-image:latest'
            }
        }

        stage('Deploy') {
          steps {
            sh 'kubectl apply -f deployment.yaml'
          }
        }

    }
}