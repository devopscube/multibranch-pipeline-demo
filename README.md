# multibranch-pipeline-demo
# Jenkins Multibranch Pipeline Example Repo 

pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }
    }
}
