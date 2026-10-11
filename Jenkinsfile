pipeline {
    agent any

    environment {
        MAVEN_HOME = 'C:\\tools\\apache-maven-3.10.0'
        DOCKER_IMAGE = 'hello-maven:1.0'
    }

    stages {
        stage('1. Verify Tools') {
            steps {
                bat 'java -version'
                bat '"%MAVEN_HOME%\\bin\\mvn.cmd" -version'
                bat 'docker version'
            }
        }

        stage('2. Maven Test') {
            steps {
                bat '"%MAVEN_HOME%\\bin\\mvn.cmd" clean test'
            }
        }

        stage('3. Maven Package') {
            steps {
                bat '"%MAVEN_HOME%\\bin\\mvn.cmd" package'
            }
        }

        stage('4. Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('5. Run Docker Container') {
            steps {
                bat 'docker run --rm %DOCKER_IMAGE%'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Maven build, tests, and Docker pipeline completed!'
        }
        failure {
            echo 'FAILED: Check the stage that failed in Console Output.'
        }
    }
}
