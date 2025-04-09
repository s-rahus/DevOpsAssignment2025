pipeline {
    agent any

    parameters {
        string(name: 'ENVIRONMENT', defaultValue: 'prod', description: 'Environment to deploy to')
    }

    environment {
        PROD_URL = 'https://prod.example.com'
        DEPLOY_SCRIPT = './deploy-prod.sh'  // Your production deploy script
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    echo "Building project for ${params.ENVIRONMENT} environment"
                    sh 'mvn clean install' // Adjust your build steps as needed
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploying to Production environment..."
                    sh DEPLOY_SCRIPT
                }
            }
        }

        stage('Test Production') {
            steps {
                script {
                    echo "Running tests on Production..."
                    sh './run-prod-tests.sh' // Adjust with your test script
                }
            }
        }
    }

    post {
        success {
            echo "Deployment to Production was successful!"
        }
        failure {
            echo "Deployment to Production failed!"
        }
    }
}