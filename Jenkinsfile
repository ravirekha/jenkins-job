pipeline {
  environment {
    registry = "uhub.service.ucloud.cn"
    registry_path = 'ws_kubernetes_mirror'
    registryCredential = 'uhub'
    ANSIBLE_VERSION = '2.4.0.0'
    TERRAFORM_VERSION = '0.11.13'
    dockerImage = ''
    imageName = "ws-jenkins-slave"
    }
  agent {
  label 'slave2'
  }
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/ravirekha/jenkins-job.git'
      }
    }
    stage('Building image') {
      steps{
        script {
         sh 'env'
         dockerImage = docker.build("${registry}/${registry_path}/${imageName}" + ":latest", "--build-arg ANSIBLE_VERSION=\"${ANSIBLE_VERSION}\" --build-arg TERRAFORM_VERSION=\"${TERRAFORM_VERSION}\" --no-cache .")
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
