pipeline {

    agent any

    options {
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
                    branches: [[name: '*/master']], 
                    userRemoteConfigs: [[url: 'https://github.com/ch680351034/multibranch-pipeline-demo.git']]
                ])
               //sh 'version=$(gitversion | jq -r '.MajorMinorPatch')'
                sh 'gitversion > version.json'
                sh 'cat version.json'
               // sh "version=$(jq -r '.MajorMinorPatch' version.json)"
                script {
                    def props = readProperties file: 'version.json'
                    println "${props['MajorMinorPatch']}"
                    currentBuild.displayName = props.MajorMinorPatch
                }
                
                //echo $version
            }
        }

        stage(' Unit Testing') {
            steps {
                sh """
                echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
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
