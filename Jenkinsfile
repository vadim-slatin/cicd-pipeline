pipeline {
  agent any
  stages {
    stage('Application Build') {
      agent any
      steps {
        sh '''chmod +x scripts/build.sh
./scripts/build.sh'''
      }
    }

    stage('Test') {
      steps {
        sh '''chmod +x scripts/test.sh
./scripts/test.sh'''
      }
    }

    stage('Docker Image Build') {
      steps {
        sh '''docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
'''
      }
    }

  }
  environment {
    IMAGE_NAME = 'my_app'
    IMAGE_TAG = 'latest'
  }
}