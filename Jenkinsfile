pipeline {

    agent {
        node {
            label 'master'
        }
    }

    options {
        skipDefaultCheckout(true)
        buildDiscarder logRotator( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
            )
    }

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }

        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/master'], [name: '*/develop'], [name: '*/feature']], 
                    userRemoteConfigs: [[url: 'https://github.com/rbullers/multibranch-pipeline-demo.git']]
                ])
            }
        }

        stage('Echo Branch Name') {
            steps {
                sh """
                echo $env.BRANCH_NAME
                echo %GIT_BRANCH%
                """
            }
        }

        stage(' Unit Testing') {
            when {
                branch 'master'
            }
            steps {
                sh """
                echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
            when {
                changeRequest target: 'develop'
            }
            steps {
                sh """
                echo "Running Code Analysis"
                """
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                sh """
                echo "Building Artifact"
                """

                sh """
                echo "Deploying Code"
                """
            }
        }

    }   
}
