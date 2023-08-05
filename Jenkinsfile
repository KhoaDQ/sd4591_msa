pipeline {
    agent any

    stages {
        stage('Build and Push Docker Images') {
            steps {
                script {
                    // Set the necessary environment variables
                    def awsRegion = 'ap-southeast-1'
                    def ecrRepo = '359145461483.dkr.ecr.ap-southeast-1.amazonaws.com/my-ecr-repo-devops'
                    def dockerImageTag = 'latest'

                    // Authenticate Docker with your ECR
                    def ecrLogin = sh(script: "aws ecr get-login-password --region ${awsRegion}", returnStdout: true).trim()
                    sh "echo '${ecrLogin}' | docker login --username AWS --password-stdin ${ecrRepo}"

                    // Build and push the Docker images
                    sh "docker build -t ${ecrRepo}/frontend:${dockerImageTag} frontend/"
                    sh "docker build -t ${ecrRepo}/backend:${dockerImageTag} backend/"
                    sh "docker push ${ecrRepo}/frontend:${dockerImageTag}"
                    sh "docker push ${ecrRepo}/backend:${dockerImageTag}"
                }
            }
        }
    }
}
