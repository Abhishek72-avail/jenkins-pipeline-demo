pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                bat 'npm install'
                echo 'Build completed'
            }
        }
        
        stage('Test') {
            steps {
                bat 'npm test'
                echo 'Tests completed'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t my-app:%BUILD_NUMBER% .'
                echo 'Docker image built'
            }
        }
        
        stage('Deploy') {
            steps {
                bat 'docker stop my-app || exit 0'
                bat 'docker rm my-app || exit 0'
                bat 'docker run -d -p 3000:3000 --name my-app my-app:%BUILD_NUMBER%'
                echo 'Application deployed'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}