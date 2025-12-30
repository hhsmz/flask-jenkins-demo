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
                // Create virtual environment
                bat '"C:\\Users\\abdul\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m venv venv'
                
                // Activate venv and install dependencies in the same command
                bat 'call venv\\Scripts\\activate.bat && python -m pip install --upgrade pip && python -m pip install -r requirements.txt'
            }
        }

        stage('Run Unit Tests') {
            steps {
                // Activate venv and run pytest in the same command
                bat 'call venv\\Scripts\\activate.bat && python -m pytest'
            }
        }

        stage('Build Application') {
            steps {
                // Prepare build folder (simulated build)
                bat 'mkdir build'
                bat 'xcopy * build /E /I /Y'
            }
        }

        stage('Deploy Application') {
            steps {
                // Deploy to target directory (simulated deployment)
                bat 'mkdir C:\\flask_deploy'
                bat 'xcopy build C:\\flask_deploy /E /I /Y'
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
