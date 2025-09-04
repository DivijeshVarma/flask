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
                bat 'C:\\Users\\Administrator\\AppData\\Local\\Programs\\Python\\Python313\\Scripts\\pip.exe install -r requirements.txt'
            }
        }

        stage('Run Application') {
            steps {
                echo 'Starting the Python web application with Gunicorn...'
                // Use 'start /b' for Windows to run Gunicorn in the background
                bat 'start /b C:\\Users\\Administrator\\AppData\\Local\\Programs\\Python\\Python313\\Scripts\\gunicorn.exe --bind 0.0.0.0:5000 app:app'
                
                // Wait for a few seconds to ensure the application starts
                sleep 5
                
                // Health check using PowerShell's Invoke-WebRequest, the Windows equivalent of curl
                echo 'Checking if the application is accessible...'
                bat 'powershell.exe -Command "Invoke-WebRequest -Uri http://localhost:5000"'
            }
        }
    }
    
}
