pipeline {
  agent any
  stages {
    stage('Application Build') {
      steps {
        sh '''chmod +x scripts/build.sh
./scripts/build.sh'''
      }
    }

    stage('Test') {
      steps {
        sh '''chmod +x scripts/test.sh
scripts/test.sh'''
      }
    }

    stage('Docker Image Build') {
      steps {
        sh 'docker build -t my_image .'
      }
    }

  }
}
