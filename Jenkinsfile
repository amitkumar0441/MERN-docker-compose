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
                    docker-compose -f docker-compose.yml build --no-cache  
                    docker-compose -f docker-compose.yml up -d  
                    """
                }
            }
        }
    }
}
