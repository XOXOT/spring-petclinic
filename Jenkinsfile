pipeline {
    agent  {
        label 'dind-agent'
    }
    stages {
        // stage('Build image') {
        //     steps {
        //         sh 'docker build -t terraform-tae/petclinic .'
        //         echo 'Build image...'
        //     }
        // }
        
        stage('Build image') {
            steps {
                dockerImage = docker.build('gcr.io/terraform-tae/petclinic')
            }
        }
        
        stage("Push image to gcr") {
            steps {
                script {
                    docker.withRegistry('https://asia.gcr.io', 'gcr:terraform-tae') {
                        dockerImage.push("${env.BUILD_NUMBER}")
                    }
                }
            }
        }

        // stage("Push image to gcr") {
        //     steps {
        //         script {
        //             catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE')
        //             {
        //               withCredentials([file(credentialsId: 'terraform-tae', variable: 'GC_KEY')]){
        //               sh "cat '$GC_KEY' | docker login -u _json_key --password-stdin https://gcr.io"
        //               sh "gcloud auth activate-service-account --key-file='$GC_KEY'"
        //               sh "gcloud auth configure-docker"
        //               GLOUD_AUTH = sh (
        //                   script: 'gcloud auth print-access-token',
        //                  returnStdout: true
        //                                         ).trim()
        //              echo "Pushing image To GCR"
        //              sh "docker push asia.gcr.io/terraform-tae/petclinic:${image-tag}"
        //              }
        //             }
        //         }               
        //     }
        // }
    }
}
