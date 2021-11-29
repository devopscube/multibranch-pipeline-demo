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
			git tag -a v1.6 -m "my version 1.6"
			git remote add origin https://github.com/akashkadao/multibranch-pipeline-demo.git
			git push --set-upstream origin develop
			'''
		}
	    }
        }     
    }
}
