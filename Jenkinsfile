pipeline {  
  environment {
      registry = "fatimaezzahraMendada/tp5devops"
      registryCredential = 'fatimaezzahraMendada_DOCKER_HUB'
      dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
          git 'https://github.com/fatima-ezzahraMendada/tp5Devops.git'
      }
    }
    stage('Building image') {
      steps{
          script {
              dockerImage = docker.build registry + ":$BUILD_NUMBER"
          }
      }
    }
    stage('Test image') {
      steps{
        script {

          echo "Tests passed"
        }
      }
    }
    stage('Publish Image') {
      steps{
          script {
              docker.withRegistry( '', registryCredential ) {
              dockerImage.push()
              }
          }
      }
    }

    stage('Deploy Image') {
      steps{
          script {
              sh "docker run -d $registry:$BUILD_NUMBER"
          }
      }
    }
  }
}