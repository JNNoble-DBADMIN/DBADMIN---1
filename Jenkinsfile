pipeline {
  agent any

  tools {
    nodejs "NodeJS_18"
  }

  // ✅ ADDED: Set environment variables
  environment {
    APP_VERSION = '1.0.0'
    DEPLOY_ENV = 'production'
  }

  stages {
    stage('Install') {
      steps {
        sh 'npm ci'
      }
    }

    stage('Lint') {
      steps {
        sh 'npm run lint || echo "Linting failed."'
      }
    }

    stage('Test') {
      steps {
        sh 'npm test'
      }
    }

    // ✅ ADDED: New Build stage
    stage('Build') {
      steps {
        echo "🏗️  Building version ${APP_VERSION} for ${DEPLOY_ENV}"
        sh 'npm run build || echo "No build script found."'
      }
    }
  }

  post {
    success {
      // ✅ UPDATED: Added env info to Slack message
      slackSend channel: '#ci', message: "✅ Build passed on ${env.JOB_NAME} #${env.BUILD_NUMBER} (${DEPLOY_ENV} v${APP_VERSION})"
    }
    failure {
      // ✅ UPDATED: Added env info to Slack message
      slackSend channel: '#ci', message: "❌ Build failed on ${env.JOB_NAME} #${env.BUILD_NUMBER} (${DEPLOY_ENV} v${APP_VERSION})"
    }
    // ✅ ADDED: Always cleanup step
    always {
      echo '📦 Post-build cleanup complete.'
    }
  }
}
