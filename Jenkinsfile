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
		withCredentials([usernamePassword(credentialsId: 'gitcreds', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
			
    			sh("git tag -a \$GIT_TAG")
    			sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@https://github.com/akashkadao/multibranch-pipeline-demo.git --tags')
		}
	    }
        }     
    }
}
