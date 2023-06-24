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
}    