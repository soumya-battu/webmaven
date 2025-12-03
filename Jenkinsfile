pipeline {
    agent any

    // Define tools installed in Jenkins
    tools {
        maven 'Maven'  // Maven installation name in Jenkins Global Tool Configuration
        jdk 'JDK'      // JDK installation name in Jenkins
    }

    environment {
        // Tomcat details
        TOMCAT_URL = 'http://localhost:8080/manager/text'  // Tomcat manager URL
        TOMCAT_USER = 'admin'       // Tomcat manager username
        TOMCAT_PASSWORD = 'admin123' // Tomcat manager password

        // GitHub PAT credential ID
        GIT_CREDENTIALS_ID = 'github-pat'
    }

    stages {
        stage('Checkout from GitHub') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/soumya-battu/webmaven.git',
                    credentialsId: "${GIT_CREDENTIALS_ID}"
            }
        }

        stage('Build with Maven') {
            steps {
                // Windows batch command
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Deploy WAR to Tomcat using Jenkins Deploy plugin
                deploy adapters: [tomcat9(
                    credentialsId: 'tomcat-cred', // Jenkins credential for Tomcat manager
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
