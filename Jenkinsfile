pipeline {

    agent any

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
            )
    }

    stages {

        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    userRemoteConfigs: [[url: 'https://github.com/srinivas325/multibranch-pipeline-demo.git']]
                ])
            }
        }

        stage(' Unit Testing') {
            steps {
                
                echo "Running Unit Tests"
             
            }
        }

        stage('Code Analysis') {
            steps {
             
                echo "Running Code Analysis"
            
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
             
                echo "Building Artifact"
            
       
                echo "Deploying Code"
           
            }
        }

    }   
}
