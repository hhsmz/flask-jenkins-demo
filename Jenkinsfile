pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/hhsmz/flask-jenkins-demo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Create Python virtual environment
                bat '"C:\\Users\\abdul\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m venv venv'
                
                // Activate venv, upgrade pip, install requirements
                bat 'call venv\\Scripts\\activate.bat && python -m pip install --upgrade pip && python -m pip install -r requirements.txt'
            }
        }

        stage('Run Unit Tests') {
            steps {
                // Activate venv and run pytest
                bat 'call venv\\Scripts\\activate.bat && python -m pytest'
            }
        }

        stage('Build Application') {
            steps {
                // Remove old build folder if it exists
                bat 'if exist build rmdir /S /Q build'

                // Create new build folder
                bat 'mkdir build'

                // Copy all files except build, venv, and .git
                bat 'robocopy . build /E /XD build venv .git'
            }
        }

        stage('Deploy Application') {
            steps {
                // Remove old deploy folder if it exists
                bat 'if exist C:\\flask_deploy rmdir /S /Q C:\\flask_deploy'

                // Create deploy folder
                bat 'mkdir C:\\flask_deploy'

                // Copy build contents to deploy folder
                bat 'robocopy build C:\\flask_deploy /E'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
