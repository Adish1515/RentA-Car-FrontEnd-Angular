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
                sh 'aws s3 sync dist/rent-a-car-app s3://YOUR_BUCKET_NAME --delete'
            }
        }
    }
}
