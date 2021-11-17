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
        stage('Auto_tagging')
        { 
            steps {
                script {
                    sh """ 
                        version= \$(git describe --tags 'git rev-list  --tags  --max-count=1')
                        #Version to get the latest tag 
                        A="\$(echo \$version|cut -d '.' -f1)"
                        B="\$(echo \$version|cut -d '.' -f2)"
                        C="\$(echo \$version|cut -d '.' -f3)"
                        if [ \$C -gt 8 ]
                            then 
                        if [ \$B -gt 8 ]
                            then                    
                            A=\$((A+1))
                            B=0 C=0 
                        else
                            B=\$((B+1))
                            C=0
                        fi
                        else
                            C=\$((C+1))
                            fi
                        echo "A[\$A.\$B.\$C]">outFile """
                        nextVersion = readFile 'outFile' 
                        echo "we will tag '${nextVersion}'" 
                        result =nextVersion.substring(nextVersion.indexOf("[")+1,nextVersion.indexOf("]"))
                        echo "we will tag '${result}'"
                }                                                                    
            }
        }
    }
}
