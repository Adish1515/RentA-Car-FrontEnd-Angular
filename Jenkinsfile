pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Adish1515/RentA-Car-FrontEnd-Angular.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Angular App') {
            steps {
                bat 'npm run build -- --configuration production'
            }
        }

        stage('Deploy to S3') {
            steps {
                bat 'aws s3 sync dist/rent-a-car-app s3://YOUR_BUCKET_NAME --delete'
            }
        }
    }
}
