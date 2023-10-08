pipeline{
    agent {
        label 'orange-pi'
    }
    // tools{
    //     // blank
    // }

    environment{
        DOCKER_USER       = 'darktang3nt'
        DOCKER_PASS       = 'dockerhub'
    }

    stages{
        stage('clean and install python'){
            steps{
                // clean workspace
                cleanWs()
            }
        }

        stage('Checkout SCM'){
            steps{
                checkout scm 
            }
        }

        stage('Clean build folder'){
            steps{
                sh 'make clean'
            }
        }

        stage('Lint and Test'){
            steps{
                sh '''
                make lint
                make test
                '''
            }
        }

        stage('build image and push'){
            steps{
                script{
                docker.withRegistry('', DOCKER_PASS){
                    sh 'make image'
                    }

            // Push docker image with latest and ${IMAGE_TAG} tags.
                docker.withRegistry('', DOCKER_PASS){
                    sh 'make push'
                }
            }
        }
    }
}
} 