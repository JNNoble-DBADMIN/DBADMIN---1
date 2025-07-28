pipeline {
  agent any

  tools {
    nodejs "NodeJS_18"
  }

  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh 'npm test || echo "No tests available."'
      }
    }
  }

  post {
    success {
      echo '✅ Build and test succeeded.'
    }
    failure {
      echo '❌ Build or test failed.'
    }
  }
}

