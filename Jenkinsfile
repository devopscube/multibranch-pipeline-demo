pipeline { 
    agent any
    stages {
        stage('Build') {
            agent {label 'build_script'}
            steps {
                sh 'echo package'
            }
        }
        stage('Test') {
            agent {label 'Test_script'}
            steps {
                sh 'echo check'
            }
        }
        stage('Deploy') {
            agent {label 'deploy_script'}
            steps {
                echo 'Deploying only because this commit is tagged...'
                sh 'echo deploy'
            }
        }
        stage('git tags') {
            environment { 
                GIT_TAG = "$BUILD_TAG" 
            }
            agent {label 'Tag_script'}
            steps {
                sh '''
                    git tag \$GIT_TAG
                   '''             
            }
        }     
    }
}
