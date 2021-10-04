pipeline {
    agent any
    stages {
        stage('Init') {
            steps{
              echo "Init stage"
            }

        }

        stage('Test') {
            steps {
              echo "dummy stage test"
              pwd
            }
        }

        stage('Deployment')
            steps{
              echo "done"
            }
    }
}
