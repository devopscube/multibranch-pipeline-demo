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
                GIT_TAG = "Release_version-$BUILD_TAG" 
                BUILD_ID = "$BUILD_ID"
                JOB_NAME = "$JOB_NAME"
            }
            steps {
                sh '''
                    git tag -a \$GIT_TAG \$BUILD_ID \$JOB_NAME
                    git tag
                     
                   '''             
            }
        }     
    }
}
