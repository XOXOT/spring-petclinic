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
        stage('Push to registry') {
            steps {
                script {
                    def build_time = new Date()
                    def sdf = new SimpleDateFormat("yyyyMMddHHmm")
                    docker.withRegistry('https://gcr.io', 'gcr:terraform-tae') {
                    dockerImage.push("${sdf.format(build_time)}-${env.BUILD_NUMBER}")
                    dockerImage.push("latest")
      }
    }
  }
}
        
    }
}
