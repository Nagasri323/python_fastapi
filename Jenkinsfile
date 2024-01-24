pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS=credentials('nagasripalukuri')
    }
    stages { 
        stage('Clone') {
            steps {
                checkout scmGit(branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Nagasri323/python_fastapi.git']])
            }
        }
        
        stage('Deploy') {
            steps {
                withDockerRegistry(credentialsId: 'nagasripalukuri', url: 'https://hub.docker.com/repository/docker/nagasripalukuri/website/general')
                sh 'docker build -t nagasripalukuri/website:latest .'
                //sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push nagasripalukuri/website:latest'
            }
        }
    }
}
