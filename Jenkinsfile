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
  stage('Crear y Subir Imagen App') { 
            steps { 
                script { 
                    dockerImage = docker.build registry + ":latest"
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                }
            } 
        }
  stage('Apply Kubernetes Files') {
      steps {
          milestone(1)
                kubernetesDeploy(
                    kubeconfigId: 'mykubeconfig',
                    configs: 'deployment',
                    enableConfigSubstitution: true
                )
        }
      }
  
  //stage('Deploying into k8s'){
  //          steps{
  //              script {
  //              kubernetesDeploy(configs: "deployment.yml", kubeconfigId: "mykubeconfig")
  //            }
  //          }
  //      }
         
}
}
