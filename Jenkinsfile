pipeline {
  agent any

  environment {
    DOCKER_IMAGE = 'jenkins-demo'
    DOCKER_TAG = "${BUILD_NUMBER}"
    REGISTRY = 'docker.io'
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
          docker.build("${REGISTRY}/nguyenjun/${DOCKER_IMAGE}:${DOCKER_TAG}")
        }
      }
    }

    stage('Push Image') {
      when {
        branch 'main'
      }
      steps {
        script {
          docker.withRegistry("https://${REGISTRY}", 'dockerhub-creds') {
            docker.image("${REGISTRY}/nguyenjun/${DOCKER_IMAGE}:${DOCKER_TAG}").push()
          }
        }
      }
    }

  }
}
