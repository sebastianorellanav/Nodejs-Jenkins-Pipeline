pipeline {
  environment { 
        registry = "sebastianorellanav/mingeso" 
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
    stage('Pruebas Unitarias') {
      steps {
        echo "Instalando las dependencias ..."
        sh "npm install"
        echo "Realizando las pruebas unitarias ..."
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
                    dockerImage = docker.build registry + ":1.$BUILD_NUMBER"
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
