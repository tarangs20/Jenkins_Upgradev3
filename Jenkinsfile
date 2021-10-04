pipeline {
    agent any
    stages {
        stage('Init') {
            steps{
              echo "Init stage"
             }
        }

        stage('File Location'){
          steps{
            sh '''
                echo " File location is"
                pwd
            '''
          }

        }

        stage('Deploy') {
            steps{
              echo "Dummy deploy"
             }
        }
    }
}
