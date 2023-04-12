pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }
    stages { 
        stage('Clone') {
            steps {
                git 'https://github.com/nileshamlapure/fastapi.git'
            }
        }
        stage('Approval-CodeOwner') {
            steps {
                script {
                    env.Release = input message: "Provide the owner approval", ok: "Done", parameters: [string(defaultValue: 'yes', name: 'Approval Status', trim: true)]
                    echo "Code Owner Approved"
                }
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'sudo docker build -t 808748/fastapi:latest .'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'sudo docker push 808748/fastapi:latest'
            }
        }
    }
}
