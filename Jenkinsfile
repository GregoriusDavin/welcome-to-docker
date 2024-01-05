pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('davingreg-dockerhub')
  }
  
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t davingreg/test4:welcome .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push davingreg/test4:welcome'
      }
    }
  }
  
  post {
    always {
      sh 'docker logout'
    }
  }
}
