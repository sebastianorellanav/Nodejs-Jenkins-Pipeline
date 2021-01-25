pipeline {
  environment { 
        registry = "sebastianorellanav/mingeso:2" 
        registryCredential = 'dockerhub_credential' 
        dockerImage = '' 
    }
  agent {label "kubepod"}

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
