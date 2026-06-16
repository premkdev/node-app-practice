pipeline {
    agent any
    stages {
         stage ('code checkout') {
            steps {
                git url: "https://github.com/premkdev/node-app-practice.git", branch:"main"
                echo "code checkout completed"
            }
            
         }
         
         stage ('docker build and deploy') {
            steps {
                sh "docker build -t node-app:latest ."
                echo "docker build completed"
            }
         }

         stage ('push image to dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                    sh "echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin"
                    sh "docker tag node-app:latest $DOCKERHUB_USERNAME/node-app:latest"
                    sh "docker push $DOCKERHUB_USERNAME/node-app:latest"
                }
                echo "image pushed to dockerhub"
            }
         }
    }
}
