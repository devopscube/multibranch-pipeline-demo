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
		    checkout([$class: 'GitSCM', branches: [[name: '*/develop']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-cred', url: 'git@github.com:akashkadao/multibranch-pipeline-demo.git']]])
		    GIT_TAG = "VersionNumber (versionNumberString: '${BUILD_DATE_FORMATTED, "yyyyMMdd"}-develop-${BUILDS_TODAY}')"
		    	sh "git tag"
			sh "git tag \$GIT_TAG"
			sh "git push origin \$GIT_TAG"
			
		}
	    }     
    }
}
