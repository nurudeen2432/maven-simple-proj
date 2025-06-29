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
        stage('Deply to dev') {
            steps {
               script {
                   def remote [name: 'jenkins-server', host: '34.201.250.49', allowAnyHost: true]
                   withCredentials([usernamePassword(credentialsId: 'server-ssh', passwordVariable: 'host-password', usernameVariable: 'host-username')]) {
                    remote.user = host-username
                    remote.password = host-password
                    sshPut remote: remote, from: 'target/maven-simple-proj-3.0-SNAPSHOT.jar', into: '/opt/tomcat/apps'
}
               }
            }
        }
    post{
        always{
            emailext body: 'test', subject: 'test', to: 'nurudeendurowade@gmail.com'
        }
    }
}
