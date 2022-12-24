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
                        sh ' mvn clean package sonar:sonar' // sends the artifacts to sonar after authentication
                    }
                }
            }
        }
        stage('Quality Gate Status') {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api-key'
                }
            }
        }
        stage('uploading artifacts to the nexus') {
            steps {
                script {
                    nexusArtifactUploader artifacts: [
                        [
                            artifactId: 'springboot',
                            classifier: '', 
                            file: 'target/Uber.jar', 
                            type: 'jar'
                        ]
                        ],
                        credentialsId: 'nexus-auth',
                        groupId: 'com.example',
                        nexusUrl: 'localhost:8081',
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        repository: 'demoapp-release',
                        version: '1.0.0'
                }
            }
        }
    }
}

