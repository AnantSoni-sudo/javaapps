pipeline {
    agent any

    tools {
        jdk 'jdk21'               // Name defined in Jenkins tool configuration
        maven 'M2_HOME'        // Name defined in Jenkins tool configuration
    }

    environment {
        PROJECT_REPO = 'https://github.com/AnantSoni-sudo/javaapps.git' 
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: "${PROJECT_REPO}"
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t my-java-app .'
            }
        }
        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 8080:8080 --name my-running-app my-java-app'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Please check the console output.'
        }
    }
}