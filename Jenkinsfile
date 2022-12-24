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
        stage('Maven build') {
            steps {
                script {
                    sh 'mvn clean install '
                }
            }
        }
        stage('static code analysis') {
            steps {
                script {
                    /* groovylint-disable-next-line NestedBlockDepth */
                    withSonarQubeEnv(credentialsId: 'sonar-api-key') {
                        sh ' mvn clean install sonar:sonar' // sends the artifacts to sonar after authentication
                    }
                }
            }
        }
    }
}
