pipeline{
    agent any
    stages{
        stage("A"){
            when{ changeRequest target: 'master' }
            steps{
                echo "========executing A========"
            }
        }
    }
    post{
        always{
            cleanWs
        }
    }
}
