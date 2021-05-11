// // podTemplate(
// //     name: 'jnlp-docker',
// //     label: 'jnlp-docker',
// //     containers: [
// //         containerTemplate(name: 'infra-docker', image: 'joao29a:jnlp-slave-alpine-docker'),
// //     ],

// // node('master') {    
// //   stage('Checkout Source') {
// //     container('infra-docker') {
// //     git 'https://github.com/justmeandopensource/playjenkins.git'
// //     }
// //   }
// //   stage('Build image') {
// //         app = docker.build("tiestovarn/myapp")
// //   }
// //   stage('Push Image') {
// //         docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {            
// //         app.push("${env.BUILD_NUMBER}")            
// //         app.push("latest") 
// //         }
// //       }
// //   stage('Deploy App') {
// //         kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "kubeconfig")
// //   }
// // })

// node {    
//       def app     
//       stage('Clone repository') {               
             
//             checkout scm    
//       }     
//       stage('Build image') {         
       
//             app = docker.build("tiestovarn/myapp")    
//        }     
//       stage('Test image') {           
//             app.inside {            
             
//              sh 'echo "Tests passed"'        
//             }    
//         }     
//        stage('Push image') {
//                                                   docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {            
//        app.push("${env.BUILD_NUMBER}")            
//        app.push("latest")        
//               }    
//            }
//         }


pipeline {  
  agent any
    stages {
      stage('Build image') {
        steps{
            sh 'docker'
            sh 'docker version'
            sh 'docker build -t docker .'
            sh 'docker image list'
            sh 'docker tag docker tiestovarn/docker:docker'
      }
    }
  }
}

//     stage('Push Image') {
//       steps{
//         script {
//           docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {            
//           dockerImage("${env.BUILD_NUMBER}")            
//           dockerImage("latest") 
//           }
//         }
//       }
//     }

//     stage('Deploy App') {
//       steps {
//         script {
//           kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "kubeconfig")
//         }
//       }
//     }

//   }

// }
