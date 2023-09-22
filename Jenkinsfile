pipeline {
    agent any

    stages {
        stage('Print Value') {
            steps {
                script {
                    def myValue = "Hello, Jenkins!"
                    echo "My value is in develop-test branch: ${myValue}"
                }
            }
        }
        // Add more stages as needed
    }
}
