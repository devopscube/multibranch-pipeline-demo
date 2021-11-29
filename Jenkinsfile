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
		sh 'git remote set-url origin https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/akashkadao/multibranch-pipeline-demo.git


            }
	}  
        stage('git tags') {
	    steps {
		withCredentials([usernamePassword(credentialsId: 'gitcreds', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
    			sh """
			git remote set-url origin https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/akashkadao/multibranch-pipeline-demo.git
			git tag -a some_tag7 -m 'Jenkins'
    			git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/akashkadao/multibranch-pipeline-demo.git --tags
			"""
		}
	    }
        }     
    }
}
