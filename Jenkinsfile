// Type Shift + Alt + F : for formatting
pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                script {
                    git 'https://github.com/Imlucky883/gawinDemoCounterApp.git'
                }
            }
        }
        stage('Unit Test') {
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }
        stage('Integration Test') {
            steps {
                script {
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
    }
}
