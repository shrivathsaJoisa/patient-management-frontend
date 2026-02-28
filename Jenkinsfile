pipeline {
  agent any

  options {
    timestamps()
    disableConcurrentBuilds()
    buildDiscarder(logRotator(numToKeepStr: '20'))
  }

  environment {
    DOCKER_BUILDKIT = '1'
    IMAGE_NAME = "patient-management-frontend:${BUILD_NUMBER}"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Docker Tools') {
      steps {
        script {
          if (isUnix()) {
            sh 'docker --version'
          } else {
            bat 'docker --version'
          }
        }
      }
    }

    stage('Frontend Image Build') {
      steps {
        script {
          if (isUnix()) {
            sh 'docker build -t ${IMAGE_NAME} .'
          } else {
            bat 'docker build -t %IMAGE_NAME% .'
          }
        }
      }
    }
  }
}
