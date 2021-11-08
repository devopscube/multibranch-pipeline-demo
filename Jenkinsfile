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
            steps {
                sh '''
                    rpmbuild --define='version ${env.BUILD_NUMBER}'
                    git tag -a v4.2 -m 'this is for release version'
                    git config --global user.email 'akashkadao@gmail.com'
                    git config --global user.name 'akashkadao'
                    git tag 
                    git push origin v4.2'''
            }
        }        
    }
}
