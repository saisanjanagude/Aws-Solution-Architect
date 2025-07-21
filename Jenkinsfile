pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'  // or whatever region you want
    }

    stages {
        stage('Checkout Git Repo') {
            steps {
                checkout scm
            }
        }

        stage('Deploy CloudFormation Stack') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'aws_s3_cloudformationdemo',
                        usernameVariable: 'AWS_ACCESS_KEY_ID',
                        passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ]) {
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
