pipeline {
  environment {
    registry = "uhub.service.ucloud.cn"
    registry_path = 'ws_kubernetes_mirror'
    registryCredential = 'uhub'
    dockerImage = ''
    imageName = "ws-jenkins-slave:latest"
    }
  agent {
  label 'docker_slave1'
  }
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/ravirekha/uhub-docker.git'
      }
    }
    stage('Building image') {
      steps{
        script {
         sh 'env'
          dockerImage = docker.build("${registry}/${registry_path}/${imageName}")
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
         sh 'env'
         docker.withRegistry( "https://${registry}", "${registryCredential}" ) {       
         dockerImage.push()
         }
        }
      }
    }
  }
} 
