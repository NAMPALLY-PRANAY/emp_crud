pipeline {
    agent any
    tools {
        maven 'Maven' // Corrected Maven tool name
        jdk 'JDK21'   // Corrected JDK tool name
    }
    environment {
        DOCKER_IMAGE = 'employeedb:latest'
        CONTAINER_NAME = 'employeedb'
        APP_PORT = '8090'
    }
    stages {
        stage('Verify Environment') {
            steps {
                echo 'Verifying environment...'
                bat 'git --version'
                bat 'mvn -version'
                bat 'docker --version'
            }
        }
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/NAMPALLY-PRANAY/emp_crud']]
                ])
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                dir('crud') { // Navigate to the subdirectory containing the pom.xml
                    bat 'mvn clean package -DskipTests'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat "docker build -t ${DOCKER_IMAGE} ."
            }
        }
        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'
                bat """
                docker stop ${CONTAINER_NAME} || exit 0
                docker rm ${CONTAINER_NAME} || exit 0
                docker run -d -p ${APP_PORT}:${APP_PORT} --name ${CONTAINER_NAME} ${DOCKER_IMAGE}
                """
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
    }
}
