pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'SonarQube'
    }

    tools {
        maven 'Maven_3.9'
        jdk 'JDK_21'
    }

    stages {
        stage('Build & Unit Tests') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Archive Build Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build, test, and analysis completed successfully!'
        }
        failure {
            echo '❌ Build failed. Check logs!'
        }
    }
}
