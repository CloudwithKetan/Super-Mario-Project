pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "your-dockerhub-username/mario:latest"
    }

    stages {

        stage('Code Pull') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/Super-Mario.git'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'docker-cred',
                        passwordVariable: 'dockerPass',
                        usernameVariable: 'dockerUser'
                    )
                ]) {
                    sh 'docker login -u $dockerUser -p $dockerPass'
                }
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
