pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('davingreg-dockerhub')
  }
  
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t davingreg/test4:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push darinpope/test4:latest'
      }
    }
  }
  
  post {
    always {
      sh 'docker logout'
    }
  }
}
