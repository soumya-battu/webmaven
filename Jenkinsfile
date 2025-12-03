pipeline {
    agent any

    environment {
        // Tomcat configuration
        TOMCAT_URL = 'http://localhost:8080/manager/text'
        TOMCAT_USER = 'admin'          // Tomcat manager username
        TOMCAT_PASSWORD = 'admin123'   // Tomcat manager password
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your code from Git
                git branch: 'main', url: 'https://github.com/yourusername/yourrepo.git'
            }
        }

        stage('Build') {
            steps {
                // Build using Maven
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Deploy using Cargo Maven plugin or Jenkins Deploy Plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcat-cred', path: '/Webpath', url: "${TOMCAT_URL}")], 
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
