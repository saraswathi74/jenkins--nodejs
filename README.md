pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/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-app.git',', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'npm test'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'npm run build'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Example: Deploy using AWS CLI, SCP, or Docker
                    // sh 'aws s3 cp build s3://your-bucket/ --recursive'
                    echo 'Deployment step here'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
