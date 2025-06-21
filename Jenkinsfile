pipeline {
    agent any
    environment {
        GITHUB_REPO = "https://github.com/WilliamDJR/sample-docker-react.git"
        DOCKERHUB_USER = "willido"
        DOCKERHUB_CREDS = "dockerhub_willido"
    }

    stages {

        stage('CheckOut Code') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: "$GITHUB_REPO"]])
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t $DOCKERHUB_USER/sample-app:jks .'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Put your testing command here if you have'
            }
        }
        stage('Publish Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: "$DOCKERHUB_CREDS", passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                    sh '''
                        docker login -u $USERNAME -p $PASSWORD
                        docker image push $USERNAME/sample-app:jks
                    '''
                }
            }
        }        
        
    }
}
