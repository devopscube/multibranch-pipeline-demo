pipeline { 
    agent any
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
        stage('git tags') {
            environment { 
                GIT_TAG = "$BUILD_TAG" 
            }
            steps {
                sh '''
                    git tag \$GIT_TAG
                    git push https://akashkadao:akashkadao@1993@https://github.com/akashkadao/multibranch-pipeline-demo.git \$GIT_TAG
                   '''             
            }
        }     
    }
}
