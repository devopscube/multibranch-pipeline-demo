pipeline {
    agent any

    stages {
        stage('Cleanup Workspace') {
            steps {
                echo "Cleaning up workspace..."
            }
        }

        stage('Code Checkout') {
            steps {
                echo "Checking out code from the repository..."
            }
        }

        stage('Unit Testing') {
            steps {
                echo "Running unit tests..."
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Running code analysis..."
            }
        }

        stage('Build Deploy Code') {
            steps {
                echo "Building and deploying code..."
            }
        }
    }
}
