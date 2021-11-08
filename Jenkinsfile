pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'make package'
            }
        }
        stage('Test') {
            steps {
                sh 'make check'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying only because this commit is tagged...'
                sh 'make deploy'
            }
        }
        stage('git tags') {
            steps {
                sh '''
                    git tag -a v3.1 -m 'this is for release version'
                    git tags -l
                    git push origin v3.1'''
            }
        }        
    }
}
