pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Python dependencies...'
                // Use the 'bat' command for Windows
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Run Application') {
            steps {
                echo 'Starting the Python web application with Gunicorn...'
                // Use 'start /b' for Windows to run Gunicorn in the background
                bat 'start /b gunicorn --bind 0.0.0.0:5000 app:app'
                
                // Wait for a few seconds to ensure the application starts
                sleep 5
                
                // Health check using PowerShell's Invoke-WebRequest, the Windows equivalent of curl
                echo 'Checking if the application is accessible...'
                bat 'powershell.exe -Command "Invoke-WebRequest -Uri http://localhost:5000"'
            }
        }
    }
    
    post {
        always {
            echo 'Performing cleanup...'
            // Use 'taskkill' to terminate the Gunicorn process on Windows
            bat 'taskkill /F /IM gunicorn.exe || exit 0'
        }
    }
}
