pipeline {
    agent any
    environment {
        BUILD_NUMBER = "${env.BUILD_NUMBER}"  // Use the Jenkins build number
    }
    stages {
        stage('Clone the Code') {
            steps {
                git branch: 'compose', url: 'https://github.com/amitkumar0441/MERN-docker-compose.git'
            }
        }
        
        stage('Build Docker Images and Run Containers') {
            steps {
                script {
                    // Pass the BUILD_NUMBER as an environment variable to Docker Compose
                    sh """
                    export BUILD_NUMBER=${BUILD_NUMBER}
                    docker-compose -f docker-compose.yml build 
                    docker-compose -f docker-compose.yml up -d  
                    """
                }
            }
        }
        stage('stage 03- push image to dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub_credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        docker login -u "$DOCKER_USER" -p "$DOCKER_PASS"
                        docker push amitkumar0441/mernproject-backend:${BUILD_NUMBER}
                        docker push amitkumar0441/mernproject-frontend:${BUILD_NUMBER}
                        docker logout
                    '''
                }
            }
        }
    }
}
