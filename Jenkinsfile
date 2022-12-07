pipeline {
  environment {
    imagename = "rudra7869/nginx"
    registryCredential = 'rudra7869-dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/rudrapratap7/nodejs-app.git', branch: 'main', credentialsId: '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'])

      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build nginx
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"

      }
    }
  }
}
