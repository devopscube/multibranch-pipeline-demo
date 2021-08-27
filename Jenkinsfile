pipeline {

    agent {
        node {
            label 'master'
        }
    }

    environment {
        IGNORE_NORMALISATION_GIT_HEAD_MOVE = "1"
        MSTEAMS_HOOK = "https://bytespackcom.webhook.office.com/webhookb2/6e1c234c-bab4-4c99-8a7b-b1b6bde15c67@21b33349-b9d3-40ae-b11f-4b49d7948a21/JenkinsCI/b8cc96b2d7df46be9cc3ef05379aa7a5/df395072-2205-4106-b733-8d0dbdf9f69a"
    }

    options {
        skipDefaultCheckout(true)
        buildDiscarder logRotator ( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
        )
        office365ConnectorWebhooks([[
                    url: "https://bytespackcom.webhook.office.com/webhookb2/6e1c234c-bab4-4c99-8a7b-b1b6bde15c67@21b33349-b9d3-40ae-b11f-4b49d7948a21/JenkinsCI/b8cc96b2d7df46be9cc3ef05379aa7a5/df395072-2205-4106-b733-8d0dbdf9f69a",
                    startNotification: true,
                    notifySuccess: true,
                    notifyFailure: true,
        ]])
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
                    branches: [[name: '*/master'], [name: '*/develop'], [name: '*/feature']], 
                    userRemoteConfigs: [[url: 'https://github.com/rbullers/multibranch-pipeline-demo.git']]
                ])
            }
        }

        stage('Echo Branch Name') {
            steps {
                sh """
                echo $env.BRANCH_NAME
                """
            }
        }

        stage('Get GitVersion Number') {
            steps {
                sh "rm -Rf .git/gitversion_cache/"
                sh "dotnet gitversion /output buildserver"
                script {
                     def props = readProperties file: 'gitversion.properties'
                     //env.GitVersion_SemVer = props.GitVersion_SemVer
                     //env.GitVersion_BranchName = props.GitVersion_BranchName
                     //env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                      env.GITTAG = props.GitVersion_MajorMinorPatch
                      //env.GitVersion_Sha = props.GitVersion_Sha
                }
            }
        }

        stage(' Unit Testing') {
            when {
                branch 'master'
            }
            steps {
                sh """
                echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
            when {
                expression {
                    env.BRANCH_NAME.contains("feature/")
                }
            }
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
                sh ''' 
                    curl https://dev01.hoststerling.com/hooks/hooks/test?token=6w2mzsTNu@rmi9Ds2z4WER4q6qfD -o log.txt
                    sed -i 's/\\x1b\\[[0-9;]*[a-zA-Z]//g' log.txt
                    rm email.html -f
                    cp ${JENKINS_HOME}/email/template.html ${JENKINS_HOME}/email/email.html
                    sed -i -e "/BUILDURL_ADDRESS/${RUN_DISPLAY_URL}"  ${JENKINS_HOME}/email/email.html
                    sed -i -e '/WEBHOOKLOG_CONTENT/{r log.txt' -e 'd}'  ${JENKINS_HOME}/email/email.html
                '''
                sh """
                    echo "Deploying Codes"
                """
                script{
                    env.CURL = readFile("log.txt")
                }
            }
        }
    }
    post {
        always {
            script {
                env.TEST = '''${DEFAULT_CONTENT}''' + "<br>" + env.CURL
            }
            emailext (
                body: '${FILE, path="${JENKINS_HOME}/email/email.html"}',
                mimeType: 'text/html',
                replyTo: '$DEFAULT_REPLYTO',
                subject: 'Test file reading',
                to: 'reece.bullers@bytespack.com'
            )
        }
    } 
}
