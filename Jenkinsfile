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
        stage("Push image to gcr") {
            steps {
                script {
                    docker.withRegistry('https://gcr.io', 'gcr:terraform-tae') {
                        app.push("${env.BUILD_NUMBER}")
        }
                }
            }
        }
        
    }
}
