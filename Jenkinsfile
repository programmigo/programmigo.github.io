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
    }
    post{
        always{
            deleteDir()
        }
    }
}
