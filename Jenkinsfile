pipeline {
  agent {
    node {
      label 'nodejs-14.15.3'
    }

  }
  stages {
    stage('build') {
      steps {
        echo 'building'
        sh 'npm install'
      }
    }

  }
}