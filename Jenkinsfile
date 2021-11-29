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
		withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'gitcreds', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME']]) {
    			sh '''
			git checkout develop
			git tag
			git tag -a v1.5 -m "my version 1.5"
			git push origin develop --tags
			'''
		}
	    }
        }     
    }
}
