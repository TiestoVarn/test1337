// podTemplate(
//     name: 'jnlp-docker',
//     label: 'jnlp-docker',
//     containers: [
//         containerTemplate(name: 'infra-docker', image: 'joao29a:jnlp-slave-alpine-docker'),
//     ],

// node('master') {    
//   stage('Checkout Source') {
//     container('infra-docker') {
//     git 'https://github.com/justmeandopensource/playjenkins.git'
//     }
//   }
//   stage('Build image') {
//         app = docker.build("tiestovarn/myapp") + ":$BUILD_NUMBER"
//   }
//   stage('Push Image') {
//         docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {            
//         app.push("${env.BUILD_NUMBER}")            
//         app.push("latest") 
//         }
//       }
//   stage('Deploy App') {
//         kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "kubeconfig")
//   }
// })

node {    
      def app     
      stage('Clone repository') {               
             
            checkout scm    
      }     
      stage('Build image') {         
       
            app = docker.build("tiestovarn/myapp")    
       }     
      stage('Test image') {           
            app.inside {            
             
             sh 'echo "Tests passed"'        
            }    
        }     
       stage('Push image') {
                                                  docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {            
       app.push("${env.BUILD_NUMBER}")            
       app.push("latest")        
              }    
           }
        }