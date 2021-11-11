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
                GIT_TAG = "Release-$BUILD_NUMBER"
            }
            steps {
                sh '''
                    git tag -a \$GIT_TAG -m 'New Tag New Build & New Build-Number'
                    git tag
                    git push --tags https://github.com/akashkadao/multibranch-pipeline-demo.git \$GIT_TAG 
                   '''             
            }
        }        
    }
}
