
pipeline {
    agent any

    stages {
        stage('1. Verify Tools') {
            steps {
                bat 'java -version'
                bat 'mvn -version'
                bat 'docker version'
            }
        }

        stage('2. Checkout Source') {
            steps {
                echo 'Source code is checked out by Jenkins'
                bat 'git --version'
            }
        }

        stage('3. Maven Test') {
            steps {
                bat 'mvn clean test'
            }
        }

        stage('4. Maven Package') {
            steps {
                bat 'mvn package'
            }
        }

        stage('5. Build Docker Image') {
            steps {
                bat 'docker build -t hello-maven:1.0 .'
            }
        }

        stage('6. Run Docker Container') {
            steps {
                bat 'docker run --rm hello-maven:1.0'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Java Maven Docker pipeline completed!'
        }
        failure {
            echo 'FAILED: Check the Jenkins Console Output.'
        }
    }
}