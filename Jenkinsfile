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
        stage('Pushing the image to the harbor'){ 
            steps{ 
                script{ 
                    sh '''
                        echo ${harbor_pass} | docker login harbor.registry.local -u admin --password-stdin
                        docker push ${IMAGE_NAME}/${IMAGE_WEB}:${IMAGE_TAG}
                    '''

                }
            }
        }
        stage('Deploying the container in the development area'){ 
            steps{ 
                script{ 
                    sh '''
                        docker compose up -d 
                    '''
                }
            }
        }
    }
}