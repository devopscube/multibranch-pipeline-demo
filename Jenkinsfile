pipeline {

    agent {
        node {
            label 'master'
        }
    }
     tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven"
    }
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
                    userRemoteConfigs: [[url: 'https://github.com/prajwalyb/microservice.git']]
                ])
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
                withSonarQubeEnv(installationName: 'SonarCloud') { // You can override the credential to be used
      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
    }
            }   
        }

        stage('Build Deploy Code') {
            when {
               
                branch 'develop'
            }
            steps {
                 git 'https://github.com/prajwalyb/microservice.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean install"

                sh """
                echo "Deploying Code"
                """
            }
        }

    }   
}

