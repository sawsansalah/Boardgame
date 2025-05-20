pipeline {
    agent any
    tools {
       jdk 'JDK17'
        maven 'Maven3'
    }


    stages {

        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }
        stage('Package') {
            steps {
                sh "mvn package"
            }
        }
    }
}
