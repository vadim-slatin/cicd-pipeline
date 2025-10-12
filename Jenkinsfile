pipeline {
    agent any

    environment {
        DOCKERHUB_USER = 'pirx'
        DOCKER_IMAGE = 'cicd-app'
        DOCKER_TAG = 'latest'
    }

    stages {
        stage('Application Build') {
            steps {
                sh '''
                    chmod +x scripts/build.sh
                    ./scripts/build.sh
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    chmod +x scripts/test.sh
                    ./scripts/test.sh
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t ${DOCKERHUB_USER}/${DOCKER_IMAGE}:${DOCKER_TAG} .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh '''
                        echo $PASS | docker login -u $USER --password-stdin
                        docker push ${DOCKERHUB_USER}/${DOCKER_IMAGE}:${DOCKER_TAG}
                        docker logout
                    '''
                }
            }
        }
    }
}