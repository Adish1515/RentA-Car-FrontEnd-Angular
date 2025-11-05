pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
        S3_BUCKET = 'rent-a-car-angular-deploy' // your S3 bucket name
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Adish1515/RentA-Car-FrontEnd-Angular.git'
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
                // Use your AWS CLI configured credentials
                sh '''
                    aws s3 sync dist/rent-a-car-app/browser s3://$S3_BUCKET --delete
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Angular app successfully deployed to S3!"
        }
        failure {
            echo "❌ Build failed!"
        }
    }
}
