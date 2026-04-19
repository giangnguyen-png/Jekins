pipeline {
  agent any

  stages {

    stage('Build') {
      steps {
        echo "Building branch: ${BRANCH_NAME}"
      }
    }

    stage('Deploy Dev') {
      when {
        branch 'develop'
      }
      steps {
        echo 'Deploying to DEV environment'
      }
    }

    stage('Deploy Prod') {
      when {
        branch 'main'
      }
      steps {
        echo 'Deploying to PRODUCTION'
      }
    }

  }
}