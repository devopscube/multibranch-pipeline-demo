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
                GIT_TAG = "Release_version-$BUILD_NUMBER"
		}
	    steps {
			sh "git tag"
			sh "git tag \$GIT_TAG"
			sh "git push origin \$GIT_TAG"
			
		}
	    }
        }     
    }
}
