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
        stage('Git checkout'){
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-login-cred', url: 'https://github.com/nurudeen2432/maven-simple-proj.git']])
                sh 'ls -lrt'
            }
        }
      }
    }
}
