# PROJECTDIS
pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
                git branch: 'main',
                url: 'https://github.com/bhaskarini99/PROJECTDIS.git'
                echo " this clones the changes made in git"
            }
        }
        stage ('pull') {
            steps {
                bat "git pull https://github.com/bhaskarini99/PROJECTDIS.git"
                bat "type README.md"
                echo " this is github"
            }
        }
    }
       post {
        always {
            emailext (
                subject: "Jenkins Build ${currentBuild.result}: ${env.JOB_NAME}",
                body: "Build ${currentBuild.result}: ${env.BUILD_URL}",
                to: "govardhanbhaskarini00@gmail.com",
                replyTo: "bhaskarinigovardhan99@gmail.com",
                mimeType: 'text/html' 
                )
            }
        }
    }
