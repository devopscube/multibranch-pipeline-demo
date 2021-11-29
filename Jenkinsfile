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
    			sh("git tag -a some_tag2 -m 'Jenkins'")
    			sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@multibranch-pipeline-demo.git --tags')
		}
	    }
        }     
    }
}
