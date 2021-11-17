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
            environment { 
                GIT_TAG = "$BUILD_TAG" 
            }
            steps {
                sh '''
                    git tag \$GIT_TAG 
                    git tag  
                   '''             
            }
        }     
        stage('Auto_tagging')
        { 
            steps {
                script {
                    sh """ 
                        git fetch --all --tags
                        version= \$(git describe --tags)
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
                    sh """
                        curl -- data '{
                        "tag_name": "${result}",
                        "target_commitish": "release",
                        "name": "${result}",
                        "body": "Release of version ${result}",
                        "draft": false, "prerelease": false}, \
                    """
                }                                                                    
            }
        }
    }
}
