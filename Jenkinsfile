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
                BUILD_ID = "${YYYY-MM-DD_hh-mm-ss}"
            }
            steps {
                sh '''
                    git tag -a \$GIT_TAG \$BUILD_ID 
                    git tag                    
                   '''             
            }
        }     
    }
}
