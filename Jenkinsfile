pipeline {
  agent any

  options {
    timestamps()
    disableConcurrentBuilds()
    buildDiscarder(logRotator(numToKeepStr: '20'))
  }

environment {
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

   
    // Build and run frontend on Vite dev server port
    stage('Build and Run') {
      steps {
        script {
          if (isUnix()) {
            sh "docker build -t ${IMAGE_NAME} ."
            sh "docker rm -f patient-mgmt-frontend || true"
            sh "docker run -d -p 5173:5173 --name patient-mgmt-frontend ${IMAGE_NAME}"
          } else {
            bat "docker build -t ${IMAGE_NAME} ."
            bat "docker rm -f patient-mgmt-frontend || ver > nul"
            bat "docker run -d -p 5173:5173 --name patient-mgmt-frontend ${IMAGE_NAME}"
          }
        }
      }
    }
    

  }
}
