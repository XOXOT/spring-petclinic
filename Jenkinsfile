pipeline {
    agent  {
        label 'dind-agent'
    }
    stages {
        stage("Build") {
            steps {
                script {
                    sh "./mvnw clean package"
                }
            }
        }
        stage("Build image") {
            steps {
                script {
                    app = docker.build("terraform-tae/petclinic")
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
