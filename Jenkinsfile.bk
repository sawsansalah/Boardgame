pipeline {
    agent any
    environment {
                scannerHome = tool 'sonar-scanner'
            }

    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sawsansalah/Boardgame.git'
            }
        }
        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }
        stage('unit test') {
            steps {
                sh "mvn test"
            }
        }
        
         stage('Trivy') {
            steps {
                sh "trivy fs --format table -o report.html ."
            }
        }
   

  
        stage('sonarqube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {

                sh '''
                $scannerHome/bin/sonar-scanner -Dsonar.projectKey=Boardgame \
                -Dsonar.projectName=Boardgame \
                -Dsonar.java.binaries="target"
                
                '''
                }
            }
        }

        
       stage('Sonarqube quility Gate Check') {
            steps {
                timeout(time: 1, unit: 'HOURS') {

                waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
               }
            }
        }
        
        stage('Deploy To Nexus') {
            steps {
              withMaven(globalMavenSettingsConfig: 'test_nexus', jdk: '', maven: '', mavenSettingsConfig: '', traceability: true) {
                 sh "mvn deploy"
               }
            }
        }
        
        stage('Build Dockerimage') {
            steps {
            script{
                withDockerRegistry(credentialsId: 'docker-creds') {
                    
                    sh "docker build -t 3788/boardgame:v1 ."
                    sh "docker push 3788/boardgame:v1 "
                    
 
                  }
               }
            }
        }
        
        stage('Deploy Docker container ') {
            steps {
            script {
                withDockerRegistry(credentialsId: 'docker-creds') {
                    
                    sh "docker run -d --name boardgame -p 8085:8080 3788/boardgame:v1"

 
                  }
               }
            }
        }
        
        
        
        
    }
}
