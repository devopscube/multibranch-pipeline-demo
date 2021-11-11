pipeline {
     properties([
          pipelineTriggers([
               [$class: 'GenericTrigger',
               genericVariables: [
               [ key: 'committer_name', value: '$.actor.displayName' ],
               [ key: 'committer_email', value: '$.actor.emailAddress' ],
               [ key: 'ref', value: '$.changes[0].refId'],
               [ key: 'tag', value: '$.changes[0].refId', regexpFilter: 'refs/tags/'],
               [ key: 'commit', value: '$.changes[0].toHash' ],
               [ key: 'repo_slug', value: '$.repository.slug' ],
               [ key: 'project_key', value: '$.repository.project.key' ],
               [ key: 'clone_url', value: '$.repository.links.clone[0].href' ]
          ],
     
               causeString: '$committer_name pushed tag $tag to $clone_url referencing $commit',
    
               token: 'abc123',
    
               printContributedVariables: true,
               printPostContent: true,
    
               regexpFilterText: '$ref',
               regexpFilterExpression: '^refs/tags/.*'
          ]
     ])
 ])
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
        stage("Email") {
             steps {
                  
                    def subject = ""
                    def bodyText = ""
                    if (currentBuild.currentResult == 'SUCCESS') {
                    subject = "Released $tag in $repo_slug"
                    bodyText = """
                    Hi there!!
    
                    You pushed $tag in $clone_url and it is now released.
                    Version $tag was built from $commit
    
                    See job here: $BUILD_URL
                    See log here: $BUILD_URL/consoleText
                    """
               } 
                    else {
                    subject = "Failed to release $tag in $repo_slug"
                    bodyText = """
                    Hi there!!
    
                    You pushed $tag in $clone_url and the release failed (${currentBuild.currentResult}).
    
                    See job here: $BUILD_URL
                    See log here: $BUILD_URL/consoleText
                    """
               }
             }
        }
    }
}
