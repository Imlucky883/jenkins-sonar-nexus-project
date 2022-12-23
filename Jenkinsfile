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
    }
}
