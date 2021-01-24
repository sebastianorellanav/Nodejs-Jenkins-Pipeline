pipeline {
  agent any
  stages {
    stage('build') {
      agent {
        node {
          label 'nodejs'
        }

      }
      steps {
        echo 'building'
        sh 'npm install'
      }
    }

  }
}