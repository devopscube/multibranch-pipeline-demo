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
                GIT_TAG = "jenkins-$BUILD_NUMBER"
            }
            steps {
                sh '''
                    git config --global user.email 'akashkadao@gmail.com'
                    git config --global user.name 'akashkadao'
                    git tag -a \$GIT_TAG -m '[Jenkins CI] New Tag'
                    git tag
                    git push origin \$GIT_TAG -u akashkadao 
                   '''               
            }
        }        
    }
}
