pipeline {
    agent any

    tools {
        maven 'MAVEN-HOME'   // Make sure this name matches Jenkins Maven installation
        jdk 'JDK'            // Make sure JDK is configured in Jenkins
    }

    environment {
        GIT_CREDENTIALS_ID = 'github-pat' // Jenkins credential for GitHub PAT
        GIT_REPO = 'https://github.com/soumya-battu/webmaven.git'
        PROJECT_DIR = 'mavenjava'         // Your project folder
    }

    stages {
        stage('Checkout & Clean') {
            steps {
                // Clone repo using Jenkins Git plugin
                git branch: 'main', url: "${GIT_REPO}", credentialsId: "${GIT_CREDENTIALS_ID}"
                
                // Clean target folder
                bat "mvn clean -f ${PROJECT_DIR}/pom.xml"
            }
        }

        stage('Install') {
            steps {
                bat "mvn install -f ${PROJECT_DIR}/pom.xml"
            }
        }

        stage('Test') {
            steps {
                bat "mvn test -f ${PROJECT_DIR}/pom.xml"
            }
        }

        stage('Package') {
            steps {
                bat "mvn package -f ${PROJECT_DIR}/pom.xml"
            }
        }
    }

    post {
        success {
            echo "Build Successful!"
        }
        failure {
            echo "Build Failed!"
        }
    }
}
