pipeline {

  environment {
    registry = "ankurjha21/python-flask-app"
    registryCredential = "232c23f1-4396-424b-b0c3-416dd6fc9ab1"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '697b1403-666a-4d37-99ca-c90b4150df32', url: 'https://github.com/ankurjha21/jenkins-docker-flask.git']]])
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          docker run registry + ":$BUILD_NUMBEr"
          "curl http://18.208.214.55:5000"
        }
      }
    }

  }

}
