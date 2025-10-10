pipeline {
  agent any
  stages {
    stage('Application Build') {
      steps {
        sh 'scripts/build.sh'
      }
    }

    stage('Test') {
      steps {
        sh 'scripts/test.sh'
      }
    }

    stage('Docker Image Build') {
      steps {
        sh 'docker build -t my_image'
      }
    }

  }
}