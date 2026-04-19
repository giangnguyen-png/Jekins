# 
pipeline {
  agent {
    docker {
      image 'node:18-alpine'
    }
  }
  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }
    stage('Lint') {
      steps {
        sh 'npm run lint'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
  }
}
