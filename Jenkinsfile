pipeline {
    agent  {
        label 'dind-agent'
    }
    stages {
        stage('Build image') {
            steps {
                sh 'docker build -t terraform-tae:$BUILD_NUMBER .'
                sh 'docker image tag terraform-tae:$BUILD_NUMBER terraform-tae:latest'
                echo 'Build image...'
            }
        }
    }
}
node {
        stage("Push image to gcr") {
            steps {
                script {
                    docker.withRegistry('https://asia.gcr.io', 'gcr:terraform-tae') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
        }
                }
            }
        }
}
