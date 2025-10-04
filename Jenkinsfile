pipeline {
    agent any

    tools {
        maven 'maven3'
        jdk 'jdk-17'
    }

    environment {
        IMAGE_NAME = "3788/boardgame"
        IMAGE_TAG = "v${env.BUILD_NUMBER}"  // dynamic version tag
        DEPLOY_FILE = "deployment-service.yaml"
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
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-hub-credentials', toolName: 'docker') {
                        sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                    }
                }
            }
        }
    }
}
        /*stage('Update Deployment YAML') {
            steps {
                script {
                    sh '''
                    echo "📝 Updating image tag in ${DEPLOY_FILE}..."
                    sed -i "s|image: .*|image: ${IMAGE_NAME}:${IMAGE_TAG}|g" ${DEPLOY_FILE}
                    echo "✅ New image line:"
                    grep "image:" ${DEPLOY_FILE}
                    '''
                }
            }
        }

        stage('Deploy to Kind') {
            steps {
                script {
                    sh '''
                    kubectl config use-context kind-jenkins
                    kubectl apply -f ${DEPLOY_FILE}
                    '''
                }
            }
        }

        stage('Cleanup Local Images') {
            steps {
                script {
                    sh '''
                    echo "🧹 Cleaning up local Docker images..."
                    docker rmi ${IMAGE_NAME}:${IMAGE_TAG} || true
                    docker image prune -f || true
                    '''
                }
            }
        }
    }


    }
*/}