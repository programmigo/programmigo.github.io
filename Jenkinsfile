pipeline{
    agent any
    stages{
        // stage("Pre"){
        //     steps{
        //         sh("printenv")
        //     }
        // }
        stage("A"){
            when{ changeRequest target: 'master' }
            steps{
                echo "========executing A========"
            }
        }
        stage("Add file to branch"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'github-token', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    script {
                        def fileName = sh(script: "echo \${RANDOM}", returnStdout: true).trim()
                        sh """
                        touch $fileName
                        git add $fileName
                        git commit -m "Added new file"
                        git push origin $CHANGE_BRANCH
                        """
                    }
                }
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
