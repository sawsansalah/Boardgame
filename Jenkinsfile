pipeline {
    agent any

    tools {
        maven 'maven3'
        jdk 'jdk-17'
    }

    stages {

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false, onlyIfSuccessful: true
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t 3788/boardgame:v1 .'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-hub-credentials', toolName: 'docker') {
                        sh 'docker push 3788/boardgame:v1'
                    }
                }
            }
        }
    }
}
