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
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t employeedb:latest .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8090:8090 --name employeedb employeedb:latest'
            }
        }
    }
}
