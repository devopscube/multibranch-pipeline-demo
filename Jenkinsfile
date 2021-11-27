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
                GIT_TAG = "Jenkins_build-$BUILD_NUMBER" 
            }
            steps {
                git branch: 'develop',
                        credentialsId: 'cred-github',
                        url: 'https://github.com/akashkadao/multibranch-pipeline-demo' 
                sh '''
                    git tag \$GIT_TAG
		    git push origin \$GIT_TAG
                   '''             
            }
        }     
    }
}
