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
                        def fileName = UUID.randomUUID().toString()
                        sh """
                        git config user.email "$USERNAME@ABCD"
                        git config user.name "Jenkins"
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
