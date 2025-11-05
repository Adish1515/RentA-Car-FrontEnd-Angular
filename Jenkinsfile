pipeline {
    agent any
    environment {
        AWS_REGION = 'ap-south-1' // your S3 bucket region
        S3_BUCKET = 'rent-a-car-angular-deploy'
    }
   stage('Checkout') {
    steps {
        checkout([$class: 'GitSCM',
                  branches: [[name: '*/main']],
                  doGenerateSubmoduleConfigurations: false,
                  extensions: [],
                  userRemoteConfigs: [[url: 'https://github.com/Adish1515/RentA-Car-FrontEnd-Angular.git']]])
    }
}

            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build Angular App') {
            steps {
                sh 'npm run build -- --configuration production'
            }
        }
        stage('Deploy to S3') {
            steps {
                withAWS(credentials: 'aws-s3-creds', region: "${AWS_REGION}") {
                    sh '''
                    aws s3 sync dist/rent-a-car-app/browser s3://${S3_BUCKET} --delete
                    '''
                }
            }
        }
    }
    post {
        success {
            echo 'Deployment completed successfully!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
