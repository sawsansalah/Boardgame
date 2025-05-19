pipeline {
    agent any
    tools {
        jdk 'jdk 17'
        maven 'maven 3'
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
