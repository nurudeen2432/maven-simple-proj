pipeline {
    agent {
        label 'ubuntu'
    }

    parameters {
        string(name: 'Branch_Name', defaultValue: 'master', description: 'Enter the branch to checkout')
        choice(name: 'CHOICES', choices: ['one', 'two', 'three'], description: 'Choose a number')
    }

    tools {
        maven 'maven_3.8'
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }

        stage('Maven Version') {
            steps {
                sh 'mvn --version'
            }
        }

        stage('Execute Bash') {
            steps {
                sh 'ls -l'
            }
        }

        stage('Git Checkout') {
            steps {
                checkout scmGit(
                    branches: [[name: "*/${params.Branch_Name}"]],
                    extensions: [],
                    userRemoteConfigs: [[
                        credentialsId: 'github-login-cred',
                        url: 'https://github.com/nurudeen2432/maven-simple-proj.git'
                    ]]
                )
                sh 'ls -lrt'
            }
        }

        stage('Deploy to Dev') {
            steps {
                script {
                    def remote = [name: 'jenkins-server', host: '34.201.250.49', allowAnyHost: true]
                    withCredentials([usernamePassword(credentialsId: 'server-ssh', passwordVariable: 'host_password', usernameVariable: 'host_username')]) {
                        remote.user = host_username
                        remote.password = host_password
                        sshPut remote: remote, from: 'target/maven-simple-proj-3.0-SNAPSHOT.jar', into: '/opt/tomcat/apps'
                    }
                }
            }
        }
    }

    post {
        always {
            emailext body: 'test', subject: 'test', to: 'nurudeendurowade@gmail.com'
        }
    }
}
