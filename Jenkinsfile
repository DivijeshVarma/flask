pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                // Jenkins automatically checks out the code, but you can explicitly use the 'checkout' step if needed
                echo 'Checking out source code...'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Python dependencies...'
                // Use the 'sh' command for Linux/macOS or 'bat' for Windows
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Application') {
            steps {
                echo 'Starting the Python web application with Gunicorn...'
                // Use the 'sh' command to run the application in the background.
                // 'nohup' and '&' are used to detach the process.
                sh 'nohup gunicorn --bind 0.0.0.0:5000 app:app &'

                // A simple wait to ensure the application starts
                sleep 5

                // Health check using curl
                echo 'Checking if the application is accessible...'
                sh 'curl --fail http://localhost:5000'
            }
        }
    }

    // Post-build actions for cleanup
    post {
        always {
            echo 'Performing cleanup...'
            // Find and kill the Gunicorn process by port number to free up resources
            sh 'lsof -i :5000 -t | xargs kill'
        }
    }
}
