pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'building'
        sh 'npm install'
      }
    }

  }
  environment {
    nodejs = 'nodejs-14.15.3'
  }
}