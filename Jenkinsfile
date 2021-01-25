pipeline {
  agent any

  tools { nodejs "nodejs"}

  stages {
    stage('Mongo'){
      steps{
        echo "Instalando mongo..."
        sh "apt update"
        sh "sudo apt install -y mongodb"
        sh "sudo systemctl status mongodb"
        sh "mongo --eval 'db.runCommand({ connectionStatus: 1 })'"
      }
    }
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
