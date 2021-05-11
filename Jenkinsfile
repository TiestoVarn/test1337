pipeline {

  environment {
    registry = "172.100.100.100:5000/justme/myweb"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/TiestoVarn/test1337'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build --privileged -v /var/run/docker.sock:/var/run/docker.sock registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
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
