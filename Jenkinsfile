// pipeline {

//   agent any

//   stages {

//     stage('Checkout Source') {
//       steps {
//         git 'https://github.com/justmeandopensource/playjenkins.git'
//       }
//     }

//     stage('Build image') {
//       steps{
//         script {
//           app = docker.build("tiestovarn/docker") + ":$BUILD_NUMBER"
//         }
//       }
//     }
//     stage('Docker Login'){
//       steps {
//         script {
//             withCredentials([string(credentialsId: 'DockerHubCreeds', variable: 'PASSWORD')]) {
//                 sh 'docker login -u tiestovarn -p $PASSWORD'
//               }
//             }
//           }
//         } 
//     stage('Push Image to Docker Hub'){
//       steps {
//         script {
//             sh 'docker push tiestovarn/docker:latest'
//           }
//         }
//       }

//     stage('Deploy App') {
//       steps {
//         script {
//           kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
//         }
//       }
//     }

//   }

// }
node {
    
        withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u tiestovarn -p $PASSWORD'
    }
    
    stage("Docker build"){
        sh 'docker build -t diplom .'
        sh 'docker image list'
        sh 'docker tag diplom tiestovarn/docker:diplom'
    }


    stage("Push Image to Docker Hub"){
        sh 'docker push  tiestovarn/docker:diplom'
    }
    stage("Deploy App"){
        sh "ls -la && pwd"
        sh kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }

}
