pipeline {
    agent any
    tools {
        jdk "jdk 17"
        maven "maven 3"
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
     }
}
