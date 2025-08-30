pipeline {
    agent any

    tools {
        maven 'Maven_3.9.6' // Make sure this name matches what you configured in Jenkins UI
    }

    environment {
        MAVEN_OPTS = "-Dmaven.repo.local=.m2/repository"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/jyotirmoy43/Banking-java-project.git'
                echo 'Checked out code from GitHub'
            }
        }

        stage('Compile Code') {
            steps {
                echo 'Starting compilation...'
                sh 'mvn compile'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('QA - Code Quality') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }

        stage('Package Application') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myimg .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -dt -p 8091:8091 --name c000 myimg'
            }
        }
    }
}
