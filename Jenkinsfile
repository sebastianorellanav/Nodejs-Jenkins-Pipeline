pipeline {
  agent any

  tools { nodejs "nodejs" }

  stages {
    stage('Build') {
      steps {
        echo "Realizando build ..."
        sh "npm install"
      }
    }
    stage('Pruebas Unitarias') {
      steps {
        sh "npm test"
      }
    }
    stage('Analisis de Código') {
      steps {
        echo "Realizando analisis de código ..."
        sh 'npm run lint'
      }
  }
}
}
