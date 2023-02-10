pipeline {
    agent any
    options {
        // Timeout counter starts AFTER agent is allocated chummybunny1337
        timeout(time: 5000, unit: 'SECONDS')
    }
    stages {
        stage('Build') {
            steps {
            dir("${JENKINS_HOME}/workspace/CI_Pipeline/test1337") {
                    sh "git checkout students"
                    sh "./mvnw spring-boot:build-image"
                }
            }
        }
        stage('TriggerDeployJob') {
            steps {
                script {
            dir("${JENKINS_HOME}/workspace/CI_Pipeline/test1337") {
                    def IMAGE_ID = sh(script: """docker images -q spring-petclinic""", returnStdout: true).trim()
                    build job: 'CD_Pipeline', parameters: [[$class: 'StringParameterValue', name: 'IMAGE_ID', value: IMAGE_ID]]
                    }
                }
            }
        }
    }
}
