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
                    git tag -a \$GIT_TAG -m '[Jenkins CI] New Tag'
                    git tag
                    git config --global user.email 'akashkadao@gmail.com'
                    git config --global user.name 'akashkadao'
                    
                   '''             
                sshagent(['my-ssh-credentials-id']) {
                    sh("""
                        #!/usr/bin/env bash
                        set +x
                        export GIT_SSH_COMMAND="ssh -o StrictHostKeyChecking=no"
                        git push origin \$GIT_TAG
                     """)
                }
            }
        }        
    }
}
