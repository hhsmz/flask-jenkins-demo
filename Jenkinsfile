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
                bat '"C:\\Users\\abdul\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m venv venv'
                bat 'call venv\\Scripts\\activate.bat && python -m pip install --upgrade pip && python -m pip install -r requirements.txt'
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat 'call venv\\Scripts\\activate.bat && python -m pytest'
            }
        }

        stage('Build Application') {
            steps {
                bat 'if exist build rmdir /S /Q build'
                bat 'mkdir build'

                // Use robocopy but ignore its return codes
                bat 'robocopy . build /E /XD build venv .git || exit 0'
            }
        }

        stage('Deploy Application') {
            steps {
                // Remove old deploy folder
                bat 'if exist C:\\flask_deploy rmdir /S /Q C:\\flask_deploy'
                bat 'mkdir C:\\flask_deploy'

                // Copy build folder contents to deploy folder, ignore robocopy return code
                bat 'robocopy build C:\\flask_deploy /E || exit 0'
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
