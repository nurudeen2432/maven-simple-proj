pipeline {
    agent {
        label 'ubuntu'
    }
    parameters{
        string(name:'Branch_Name', defaultValue:'master', description: 'Enter the branch to checkout')
        choice(name:'CHOICES', choices: ['one', 'two', 'three'], description: 'choose a number')
    }

    tools{
        maven 'maven_3.8'
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    stage('mvn version') {
            steps {
                sh 'mvn --version'
            }
        }

        stage('Execute Bash') {
            steps {
                sh 'ls -l'
            }
        }

        stage('Git checkout') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/master']],
                    extensions: [],
                    userRemoteConfigs: [[
                        credentialsId: 'github-login-cred',
                        url: 'https://github.com/nurudeen2432/maven-simple-proj.git'
                    ]]
                )
                sh 'ls -lrt'
            }
        }
    }
    post{
        always{
            emailext body: 'test', subject: 'test', to: 'nurudeendurowade@gmail.com'
        }
    }
}
