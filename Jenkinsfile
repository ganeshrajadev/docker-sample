pipeline {
  agent {
        docker {
            image 'node:13.12.0-alpine'
            args '-p 3000:3000'
        }
    }
  environment {
 registry = 'ganeshraja10/sample-backend'
 registryCredential = 'dockerid'
 dockerImage = ''
  }
  agent any
  stages {
    // stage('Cloning Git') {
    //   steps {
    //     // git 'https://github.com/ganeshraja10/docker-sample.git'
    //   }
    // }
    stage('Building image') {
      steps{
        script{
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push to Docker hub') {
      steps{
        script{
          docker.withRegistry( '', registryCredential ) {
            // dockerImage.push()
          }
        }
      }
    }
    stage('Remove Previous docker images') {
      steps{
        sh 'docker-compose down'
      }
    }
    stage('Deploy Latest docker images') {
      steps{
        sh 'docker-compose up -d'
      }
    }
  }
}