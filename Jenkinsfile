pipeline {
    agent any

    tools {
        maven 'Maven 3.9.11'
        jdk 'C:\\Program Files\\Java\\jdk-17'
    }

    stages {
        stage('Checkout & Clean') {
            steps {
                git branch: 'main', url: 'https://github.com/soumya-battu/webmaven.git'
                bat "mvn clean"
            }
        }

        stage('Install') {
            steps {
                bat "mvn install"
            }
        }

        stage('Test') {
            steps {
                bat "mvn test"
            }
        }

        stage('Package') {
            steps {
                bat "mvn package"
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
