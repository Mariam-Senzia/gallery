pipeline {
    
    agent any
    
    tools {
        nodejs '20.3.1'
    }

    environment {
        CI = 'true'
    }

    stages {
        
        stage('clone repository') {
            steps {
                git 'https://github.com/Mariam-Senzia/gallery.git'
            }
        }

        stage('Build the project') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Tests') {
            steps {
                sh 'npm test'
            }
        }
        
        stage('Deploy to Heroku') {
            steps {
                withCredentials([usernameColonPassword(credentialsId: 'heroku', variable: 'HEROKU_CREDENTIALS')]){
                    sh "git push https://${HEROKU_CREDENTIALS}@git.heroku.com/hidden-mesa-66583.git"
                } 
            }
        }
    }

    post {
        failure {
            emailext body: 'Test fail', subject: 'Test', to: 'mariasenzia@gmail.com'
        } 

        success {
            slackSend channel: 'mariam_ip1', message: "Build id: ${BUILD_ID} | Heroku link :'https://hidden-mesa-66583-bcc6c745b126.herokuapp.com/'"
        }
    }
}    