pipeline {
    agent any

    tools {
        jdk 'JDK 21'               // Name defined in Jenkins tool configuration
        maven 'Maven 3.9.6'        // Name defined in Jenkins tool configuration
    }

    environment {
        PROJECT_REPO = 'https://github.com/AnantSoni-sudo/javaapps.git'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: "${PROJECT_REPO}"
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
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
