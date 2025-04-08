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
                sh 'npm install'
                echo 'Build completed'
            }
        }
        
        stage('Test') {
            steps {
                sh 'npm test'
                echo 'Tests completed'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app:${BUILD_NUMBER} .'
                echo 'Docker image built'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'docker stop my-app || true'
                sh 'docker rm my-app || true'
                sh 'docker run -d -p 3000:3000 --name my-app my-app:${BUILD_NUMBER}'
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