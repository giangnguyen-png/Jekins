pipeline {
  agent any

  environment {
    DOCKER_IMAGE = 'nguyenjun/jenkins-demo'
    DOCKER_TAG = "${BUILD_NUMBER}"
  }

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Test') {
      agent {
        docker { image 'node:18' }
      }
      steps {
        sh 'npm ci'
        sh 'npm test'
      }
    }

    stage('Build Image') {
      steps {
        script {
          docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
        }
      }
    }

    stage('Push Image') {
      when {
        branch 'main'
      }
      steps {
        script {
          docker.withRegistry('', 'dockerhub-creds') {
            docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").push()
          }
        }
      }
    }

  }
}
