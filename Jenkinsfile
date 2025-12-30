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
                bat 'mkdir build'
                bat 'robocopy . build /E /XD build venv .git'
            }
        }

        stage('Deploy Application') {
            steps {
                bat 'mkdir C:\\flask_deploy'
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
