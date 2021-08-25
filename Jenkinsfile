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

    environment {
        IGNORE_NORMALISATION_GIT_HEAD_MOVE = "1"
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
                """
            }
        }

        stage('Get GitVersion Number') {
            steps {
                sh "rm -Rf .git/gitversion_cache/"
                sh "dotnet gitversion /output buildserver"
                script {
                     def props = readProperties file: 'gitversion.properties'
                     //env.GitVersion_SemVer = props.GitVersion_SemVer
                     //env.GitVersion_BranchName = props.GitVersion_BranchName
                     //env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                      env.GITTAG = props.GitVersion_MajorMinorPatch
                      //env.GitVersion_Sha = props.GitVersion_Sha
                }
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
                expression {
                    env.BRANCH_NAME.contains("feature/")
                }
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
