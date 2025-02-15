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
                    // Check if any python process is running and stop it
                    bat 'tasklist | findstr /I "python.exe" >nul && taskkill /F /IM python.exe /T || echo No python process found.'
                }
            }
        }

        stage('Run Flask Application') {
            steps {
                script {
                    // Run Flask app on port 5000
                    bat 'start /B python app.py'
                }
            }
        }
    }
}
