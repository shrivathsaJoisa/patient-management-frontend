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

   
    //add stage to build and run on port 80
    stage('Build and Run') {
      steps {
        script {
          if (isUnix()) {
            sh "docker build -t ${IMAGE_NAME} ."
            sh "docker run -d -p 80:80 --name patient-mgmt-frontend ${IMAGE_NAME}"
          } else {
            bat "docker build -t ${IMAGE_NAME} ."
            bat "docker run -d -p 80:80 --name patient-mgmt-frontend ${IMAGE_NAME}"
          }
        }
      }
    }
    

  }
}
