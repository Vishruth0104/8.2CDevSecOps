pipeline {
    agent any

    environment {
        NODE_ENV = "development"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Fetch the source code from the directory path specified by the environment variable'
                echo 'Compile the code and generate any necessary artefacts'
                sh 'mkdir -p build && echo "Compiled code" > build/app.txt'
            }
        }
        stage('Test') {
            steps {
                echo 'Running Unit tests'
                echo 'Running Integration tests'
            }
        }
        stage('Code Quality Check') {
            steps {
                echo 'Check the quality of the code'
            }
        }
        stage('Security Scan - npm audit') {
            steps {
                echo 'Running npm audit...'
                sh 'npm install'
                sh 'npm audit --audit-level=low'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'cp build/app.txt /tmp/deploy_app.txt'
            }
        }
        stage('Approval') {
            steps {
                echo 'Waiting for manual approval...'
                sleep time: 5, unit: 'SECONDS'
                echo 'Approval granted'
            }
        } 
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
