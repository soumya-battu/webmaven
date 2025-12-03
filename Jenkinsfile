pipeline {
    agent any

    environment {
        // Tomcat configuration
        TOMCAT_URL = 'http://localhost:8080/manager/text' // Change if needed
        TOMCAT_USER = 'admin'          // Tomcat manager username
        TOMCAT_PASSWORD = 'admin123'   // Tomcat manager password
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub using PAT stored in Jenkins credentials
                git branch: 'main',
                    url: 'https://github.com/soumya-battu/webmaven.git',
                    credentialsId: 'github-pat'  // ID of your GitHub PAT credential
            }
        }

        stage('Build') {
            steps {
                // Build using Maven
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Deploy WAR to Tomcat using Jenkins Deploy Plugin
                deploy adapters: [tomcat9(
                    credentialsId: 'tomcat-cred', // Jenkins credential ID for Tomcat manager
                    path: '/Webpath',
                    url: "${TOMCAT_URL}"
                )],
                contextPath: '/Webpath',
                war: '**/target/*.war'
            }
        }
    }

    post {
        success {
            echo 'Build and Deployment Successful!'
        }
        failure {
            echo 'Build or Deployment Failed!'
        }
    }
}
