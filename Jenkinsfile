pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/justmeandopensource/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          app = docker.build("tiestovarn/docker") + ":$BUILD_NUMBER"
        }
      }
    }
    stage("Docker Login"){
            withCredentials([string(credentialsId: 'DockerHubCreeds', variable: 'PASSWORD')]) {
                sh 'docker login -u tiestovarn -p $PASSWORD'
            }
        } 
    stage("Push Image to Docker Hub"){
            sh 'docker push tiestovarn/docker:latest'
        }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}