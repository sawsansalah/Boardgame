pipeline {
    agent any
     tools {
         maven 'maven3'
     }
    stages {

        stage('comile') {
            steps {
                dir('keys') {

                sh 'mvn compile'
                }
            }
        }
        stage('Tests') {
            steps {
                sh 'mvn test'
            }
        }
        stage('package') {
            steps {
                sh 'mvn package'
            }
        }

    }
}
