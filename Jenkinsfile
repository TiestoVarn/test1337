node {

    checkout scm

    docker.withRegistry('https://registry.hub.docker.com', 'DockerHubCreeds') {

        def customImage = docker.build("tiestovarn/docker")

        /* Push the container to the custom Registry */
        customImage.push()
    }
}