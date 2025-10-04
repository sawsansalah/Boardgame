pipeline {
    agent  any
    tools {
        maven 'maven3'
        jdk 'jdk-17'

    }
    stages {

        stage('compile') {
            steps {
                sh "mvn compile"
            }
        }
        stage('test') {
            steps {
                sh "mvn test"
            }
        }
        stage('package') {
            steps {
                sh "mvn package"
            }
        }
       stage('Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false, onlyIfSuccessful: true
            }
        }

        stage('Build  Dockerfile') {
            steps {
                 sh 'docker build -t boardgame:v1 .'
            }
        }
        
    }
}
