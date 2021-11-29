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
			git tag -a some_tag12 -m 'Jenkins'
    			git -c core.askpass=true push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/akashkadao/multibranch-pipeline-demo.git some_tag12
			'''
		}
	    }
        }     
    }
}
