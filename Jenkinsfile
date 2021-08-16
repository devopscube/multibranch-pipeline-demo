pipeline {

    agent {
        node {
            label 'master'
        }
    }

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
            )
    }

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }

        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/spring-projects/spring-petclinic.git']]
                ])
            }
        }

        stage(' Unit Testing') {
            steps {
                sh """
                echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                echo "Running Code Analysis"
                """
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                sh """
                echo "Building Artifact"
                """

                sh """
                echo "Deploying Code"
                """
            }
        }
        stage(‘Auto tagging’){ 
            
            steps {
                
                script {
                    
                    sh “”” 
                    version=\$(git describe — tags `git rev-list — tags — max-count=1`)
                    #Version to get the latest tag 
                    A=”\$(echo \$version|cut -d ‘.’ -f1)”
                    B=”\$(echo \$version|cut -d ‘.’ -f2)”
                    C=”\$(echo \$version|cut -d ‘.’ -f3)”
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
                    echo “A[\$A.\$B.\$C]”>outFile “””
                    nextVersion = readFile ‘outFile’ 
                    echo “we will tag ‘${nextVersion}’” 
                    result =nextVersion.substring(nextVersion.indexOf(“[“)+1,nextVersion.indexOf(“]”);
                    echo “we will tag ‘${result}’”  
                                                                        
          }                                                           
       }
    }   
}
