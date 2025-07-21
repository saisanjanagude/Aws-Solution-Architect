pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws_s3_cloudformationdemo')
        AWS_SECRET_ACCESS_KEY = credentials('aws_s3_cloudformationdemo')
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {
        stage('Checkout Git Repo') {
            steps {
                checkout scm
            }
        }

        stage('Deploy CloudFormation Stack') {
            steps {
                script {
                    sh '''
                        aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
                        aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
                        aws configure set default.region $AWS_DEFAULT_REGION

                        aws cloudformation deploy \
                          --stack-name MyS3BucketStack \
                          --template-file "AWS Cloudformation Templates/S3_Creation.yml" \
                          --capabilities CAPABILITY_NAMED_IAM
                    '''
                }
            }
        }
    }
}
