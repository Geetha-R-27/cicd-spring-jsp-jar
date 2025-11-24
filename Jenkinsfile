pipeline {
    agent any

    tools {
        maven 'maven'
    }

    environment {
        SHARED_DIR = "/var/shared-app"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Geetha-R-27/cicd-spring-jsp-jar.git'
            }
        }

        stage('Build Spring Boot App') {
            steps {
                sh "mvn clean package -DskipTests"
            }
        }

        stage('Copy JAR to Shared Folder') {
            steps {
                script {
                    JAR = sh(script: "ls target/*.jar | head -n 1", returnStdout: true).trim()
                    sh "cp ${JAR} ${SHARED_DIR}/app.jar"
                }
            }
        }

        stage('Notify') {
            steps {
                echo "JAR copied successfully. App server will pick new version automatically."
            }
        }
    }

    post {
        success {
            echo "🚀 Deployment Complete!"
        }
        failure {
            echo "❌ Deployment Failed!"
        }
    }
}
