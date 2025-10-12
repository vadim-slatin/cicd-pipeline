pipeline {
  agent any
  stages {
    stage('Application Build') {
      agent any
      steps {
        sh '''chmod +x scripts/build.sh
'''
        sh 'scripts/build.sh'
      }
    }

    stage('Test') {
      steps {
        sh '''chmod +x scripts/test.sh
'''
        sh 'scripts/test.sh'
      }
    }

    stage('Docker Image Build') {
      steps {
        sh '''docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .
'''
      }
    }

  }
  environment {
    DOCKER_IMAGE = 'pirx/cicd'
    DOCKER_TAG = '${env.BUILD_NUMBER}'
  }
}