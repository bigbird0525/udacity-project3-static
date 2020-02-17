pipeline {
    agent any
    stages {
        stage('Upload to AWS') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    sh """
                            mkdir -p ~/.aws
                            echo "[default]" > ~/.aws/credentials
                            echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" > ~/.aws/credentials
                            echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}" > ~/.aws/credentials
                    """
                    }
            }
        }
        stage('Upload to AWS') {
            steps {
                withAWS(region:'us-east-1',credentials:'jenkins') {
                s3Upload(pathStyleAccessEnabled:true, payloadSigningEnabled: true, file:'index.html', bucket:'aravn-udacity-project3')
                }
            }
        }
    }
}