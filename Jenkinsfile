pipeline { 
    agent any
    environment {
         SERVER_CEDENTIALS = credentials('gitcreds')
    }
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
                withCredentials([
                        usernamePassword(credentials: 'gitcreds', usernameVariable: USER, passwordVariable: PWD)    
		]) {
			sh '''
                    	git tag \$GIT_TAG
		    	git push origin \$GIT_TAG
                   '''     
		}
            }
        }     
    }
}
