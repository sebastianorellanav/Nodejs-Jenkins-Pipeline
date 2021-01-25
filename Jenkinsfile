pipeline {
  agent any

  tools { nodejs "nodejs"
          mongodb "mongodb"}

  stages {
    stage('Build') {
      steps {
        echo "Realizando build ..."
        sh "npm install"
        sh ""
      }
    }
    stage('Pruebas Unitarias') {
      steps {
        echo "Realizando pruebas unitarias ..."
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
