pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *')   // Poll SCM every 5 minutes
        cron('0 * * * *')        // Run build every hour
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/vynavi/FlaskApp.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    bat 'pip install -r requirements.txt' 
                }
            }
        }

        stage('Stop Existing Flask App') {
            steps {
                script {
                    bat 'taskkill /F /IM python.exe /T'  
                }
            }
        }

        stage('Run Flask Application') {
            steps {
                script {
                    bat 'start /B python app.py' 
                }
            }
        }
    }
}
