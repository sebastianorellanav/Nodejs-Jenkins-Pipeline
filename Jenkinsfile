pipeline {
  environment { 
        registry = "sebastianorellanav/mingeso:1.3" 
        registryCredential = 'dockerhub_credential' 
        dockerImage = '' 
    }
  agent any

  tools { nodejs "nodejs" }

  stages {
    stage('Repositorio Git') {
      steps {
        echo "Analizando los cambios del Respositorio..."
        git([url: 'https://github.com/sebastianorellanav/Nodejs-Jenkins-Pipeline.git', branch: 'main', credentialsId: 'github_token'])
      }
    }
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
  stage('Building our image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry
                }
            } 
        }
        stage('Deploy our image') {             steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
            }
        } 
}
}
