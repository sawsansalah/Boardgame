pipeline {
    agent  any
    tools {
        maven 'maven3'
        jdk   'java17'
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
       stage('Docker Push Image') {
           steps {
               script {
                   withDockerRegistry(credentialsId: 'docker-hub-credentials', toolName: 'docker') {
                       sh "docker build -t 3788/boardwebapp:latest ."
                       sh "docker push 3788/boardwebapp:latest"
                   }
               }
           }
       }

}
}

