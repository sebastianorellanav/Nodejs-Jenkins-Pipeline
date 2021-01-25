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
      agent { label 'docker' }
      environment {
        MONGODB_TEST_URL = 'mongodb://mongoadmin:mongopass@mongodb:27017/feathers-test?authSource=admin'
      }
      steps {
        script {
          docker.image('mongo')
            .withRun('-e "MONGO_INITDB_ROOT_USERNAME=mongoadmin" -e "MONGO_INITDB_ROOT_PASSWORD=mongopass"') {c ->
            docker.image('node:10-alpine').inside("--link ${c.id}:mongodb") {
              sh 'npm run test'
            }
          }
        }
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
