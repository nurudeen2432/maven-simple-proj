pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    stage('Execute Bash') {
        steps {
            script{
            sh 'ls -l'
            }
        }
      }
    }
}
