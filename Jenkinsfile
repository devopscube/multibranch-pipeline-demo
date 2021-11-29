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
		withCredentials([usernamePassword(credentialsId: 'gitcreds', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
    			sh("git remote set-url origin git@github.com:akashkadao/multibranch-pipeline-demo.git")
			sh("git tag -a some_tag7 -m 'Jenkins'")
    			sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/akashkadao/multibranch-pipeline-demo.git --tags')
		}
	    }
        }     
    }
}
