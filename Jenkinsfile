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

        stage('Build credit-demo image')  {
            steps {
                script {
                    dockerImage = docker.build('gcr.io/petclinic')
                }
            }
        }

        stage('Push to registry') {
            steps {
                script {
                    docker.withRegistry('https://gcr.io', 'gcr:terraform-tae') {
                    dockerImage.push("${env.BUILD_NUMBER}")
                    dockerImage.push("latest")
                    }
                }
            }
        }
        
    }
}
