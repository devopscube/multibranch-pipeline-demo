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
		withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'gitcreds', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME']]) {
    			sh "git checkout develop"
			sh "git tag"
			sh "git tag " + versionLabel
			sh "git push --set-upstream origin"
			
		}
	    }
        }     
    }
}
