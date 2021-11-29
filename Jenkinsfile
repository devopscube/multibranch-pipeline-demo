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
		withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
			sh("git config --global user.email "akashkadao@gmail.com"")
			sh("git config --global user.name "akashkadao"")
    			sh("git tag -a some_tag5 -m 'Jenkins'")
    			sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/akashkadao/multibranch-pipeline-demo --tags')
		}
	    }
        }     
    }
}
