node {

    stage("Git Clone"){

        git credentialsId: 'GitHubCreeds', url: 'https://github.com/TiestoVarn/test1337.git'
    }

     stage('Gradle Build') {

       sh './gradlew build'

    }

    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t docker .'
        sh 'docker image list'
        sh 'docker tag docker tiestovarn/docker:docker'
    }

    withCredentials([string(credentialsId: 'DockerHubCreeds', variable: 'PASSWORD')]) {
        sh 'docker login -u tiestovarn -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  tiestovarn/docker:docker'
    }

    stage("SSH Into k8s Server") {
        def remote = [:]
        remote.name = 'K8S master'
        remote.host = '100.0.0.2'
        remote.user = 'vagrant'
        remote.password = 'vagrant'
        remote.allowAnyHosts = true

        stage('Put k8s-spring-boot-deployment.yml onto k8smaster') {
            sshPut remote: remote, from: 'k8s-spring-boot-deployment.yml', into: '.'
        }

        stage('Deploy spring boot') {
          sshCommand remote: remote, command: "kubectl apply -f k8s-spring-boot-deployment.yml"
        }
    }

}

}
