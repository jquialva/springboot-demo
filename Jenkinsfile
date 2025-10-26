pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'git@github.com:jgutalva/springboot-demo.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew clean build -x test'
            }
        }
        
        stage('Test') {
            steps {
                sh './gradlew test'
            }
            post {
                always {
                    junit 'build/test-results/test/*.xml'
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline completed for Spring Boot application'
        }
        success {
            echo 'Build successful!'
            archiveArtifacts 'build/libs/*.jar'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
