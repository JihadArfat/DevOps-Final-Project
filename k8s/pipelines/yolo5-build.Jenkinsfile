pipeline {
    agent any

    environment {
        ECR_URL = "533267198104.dkr.ecr.us-east-1.amazonaws.com"
    }

    stages{
        stage('Build') {
            steps {
                sh '''
                cd k8s/yolo5
                aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 533267198104.dkr.ecr.us-east-1.amazonaws.com
                docker build -t $ECR_URL/prod/yolo5:0.0.$BUILD_NUMBER .
                docker push $ECR_URL/prod/yolo5:0.0.$BUILD_NUMBER
                '''
            }
        }
        stage('Trigger Release') {
            steps {
                build job: 'ReleaseProd', wait: false, parameters: [
                    string(name: 'IMG_URL', value: "${ECR_URL}/prod/yolo5:0.0.${BUILD_NUMBER}")
                ]
            }
        }
    }
}