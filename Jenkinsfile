pipeline {
  agent any

  tools { nodejs "nodejs" }

  stages {
    stage('Test npm') {
      steps {
        sh """
          npm --version
          node -v
        """
      }
    }
  }
}
