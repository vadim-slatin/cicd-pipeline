pipeline {
  agent any

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
            sh 'docker build -t my_app .'
        }
    }

    stage('Docker Push') {
        steps {
          withCredentials([usernamePassword(
            credentialsId: 'dockerhub-token', 
            usernameVariable: 'DOCKERHUB_USERNAME',
            passwordVariable: 'DOCKERHUB_PASSWORD'
            )]) {
            sh '''
              echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin
              docker tag my_app $DOCKERHUB_USERNAME/my_app:latest
              docker push $DOCKERHUB_USERNAME/my_app:latest
            '''
          }
      }
  }
}
}