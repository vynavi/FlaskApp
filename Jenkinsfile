pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *')   // Poll SCM every 5 minutes
        cron('0 * * * *')        // Run build every hour
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'file:///C:/Users/vynub/OneDrive/Desktop/Jenkins/flask_app'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    bat 'pip install -r requirements.txt' // Use 'sh' for Linux
                }
            }
        }

        stage('Stop Existing Flask App') {
            steps {
                script {
                    bat 'taskkill /F /IM python.exe /T'  // Stops any running Flask process (Windows)
                }
            }
        }

        stage('Run Flask Application') {
            steps {
                script {
                    bat 'start /B python app.py' // Runs Flask in background
                }
            }
        }
    }
}
