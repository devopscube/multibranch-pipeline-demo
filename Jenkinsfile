pipeline { 
    agent any
    label "my-defined-label"
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
                   '''             
            }
        }     
    }
}
