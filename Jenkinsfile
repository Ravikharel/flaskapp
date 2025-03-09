pipeline{
    agent any
    environment{ 
        IMAGE_NAME = "harbor.registry.local/flaskproject"
        IMAGE_WEB = "web"
        IMAGE_TAG = "v1"
        harbor_pass = "Harbor12345"
    }
    stages{
        stage('Building the image'){ 
            steps{ 
                script{ 
                    sh "docker image build -t ${IMAGE_NAME}/${IMAGE_WEB}:${IMAGE_TAG} ."
                }
            }

        }
        stage("Scanning through trivy"){ 
            steps{ 
                script{ 
                    sh " trivy image --exit-code 1 --severity HIGH,critical --ignore-unfixed ${IMAGE_NAME}/${IMAGE_WEB}:${IMAGE_TAG}"
                }
            }
        }
    }
}