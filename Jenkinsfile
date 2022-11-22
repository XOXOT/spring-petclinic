pipeline {
    agent  {
        label 'dind-agent'
    }
    stages {
        stage("Build") {
            steps {
                script {
                    sh "./mvnw clean install"
                }
            }
        }
        stage("Build image") {
            steps {
                script {
                    dockerImage = docker.build('gcr.io/terraform-tae/petclinic')
                }
            }
        }
        
    }
}
