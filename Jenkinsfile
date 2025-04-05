pipeline {
    agent any

    environment {
        // Optional environment variables
        PROJECT_NAME = "MyProject"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code from Git..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building the application..."
                // Add your build commands here
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                // Add test commands here
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application..."
                // Add deploy logic here
            }
        }
    }

    post {
        success {
            echo 'Pipeline finished successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
