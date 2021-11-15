pipeline { 
    agent any
    parameters {
        gitParameter name: 'BRANCH_TAG', 
                     type: 'PT_BRANCH_TAG',
                     defaultValue: 'develop'
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo package'
            }
        }
        stage('Test') {
            steps {
                sh 'echo check'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying only because this commit is tagged...'
                sh 'echo deploy'
            }
        }
        stages {
        stage('Example') {
            steps {
                checkout([$class: 'GitSCM', 
                          branches: [[name: "${params.BRANCH_TAG}"]], 
                          doGenerateSubmoduleConfigurations: false, 
                          extensions: [], 
                          gitTool: 'Default', 
                          submoduleCfg: [], 
                          userRemoteConfigs: [[url: 'https://github.com/akashkadao/multibranch-pipeline-demo.git']]
                        ])
            }
        }
    }
    }
}
