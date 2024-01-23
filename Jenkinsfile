pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS=credentials('nagasripalukuri')
    }
    stages { 
        stage('Clone') {
            steps {
                git 'https://github.com/Nagasri323/python_fastapi.git'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'sudo docker build -t nagasripalukuri/website:latest .'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'sudo docker push nagasripalukuri/website:latest'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'kubectl apply -f Kubernetes.yml'
            }
        }
    }
}
