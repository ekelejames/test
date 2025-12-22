pipeline{
    agent any 

    environment{
        APP_NAME = "test-spp"
        RELEASE = "1.0.0"
        DOCKER_USER = "ekelejay"
        DOCKER_PASS = "dockerhub"
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    }

    stages{
        stage("Cleanup workspace"){
            steps{
                cleanWs()
            }
        }

        stage("Checkout from SCM"){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/ekelejames/test'
            }
        }

        stage("Build and push docker image"){
            steps{
                script{
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.push ("${IMAGE_TAG}")
                    }

                }

            }
        }

    }
}