pipeline {
    agent any

    tools {
        maven 'Maven 3.9.11'       // Use the exact name from Jenkins configuration
        jdk 'C:\\Program Files\\Java\\jdk-17'  // Use exact JDK path or configured name
    }

    environment {
        GIT_CREDENTIALS_ID = 'github-pat' // Jenkins credential for GitHub PAT
        GIT_REPO = 'https://github.com/soumya-battu/webmaven.git'
        PROJECT_DIR = 'mavenjava'         // Your project folder
    }

    stages {
        stage('Checkout & Clean') {
            steps {
                git branch: 'main', url: "${GIT_REPO}", credentialsId: "${GIT_CREDENTIALS_ID}"
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
