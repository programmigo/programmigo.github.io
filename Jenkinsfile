pipeline{
    agent any
    stages{
        stage("Pre"){
            steps{
                sh("printenv")
            }
        }
        stage("A"){
            when{ changeRequest target: 'master' }
            steps{
                echo "========executing A========"
            }
        }
        stage("Add results to PR"){
            when{ changeRequest target: 'master' }
            steps{
                script{
                    pullRequest.comment('Tests passed...')
                }
            }
        }
    }
    post{
        always{
            deleteDir()
        }
    }
}
