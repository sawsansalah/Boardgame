pipeline {
    agent any
    tools {
        jdk "jdk 17"
        maven "maven 3"
    }
    stages {
        stage('Git') {
            steps {
               git branch: 'main', url: 'https://github.com/aziz0114/Boardgame.git'
            }
         }
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
