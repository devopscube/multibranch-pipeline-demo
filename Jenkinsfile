pipeline { 
    agent any
    environment {
        NEW_VERSION = '1.2.0'
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo package'
                sh 'echo build version ${$NEW_VERSION}'
            }
        }
        stage('Test') {
            steps {
                sh 'echo check'
                sh 'echo Test version ${$NEW_VERSION}'
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
                   '''             
            }
        }     
    }
}
