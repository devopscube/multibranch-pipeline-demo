pipeline { 
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo package'
                label 'building process'
            }
        }
        stage('Test') {
            steps {
                sh 'echo check'
                label 'Test process'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying only because this commit is tagged...'
                sh 'echo deploy'
                label 'deploy on pre-prod'
            }
        }
        stage('git tags') {
            environment { 
                GIT_TAG = "$BUILD_TAG" 
            }
            steps {
                sh '''
                    git tag \$GIT_TAG
                    label 'tagging'
                   '''             
            }
        }     
    }
}
