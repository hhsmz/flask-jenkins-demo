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
                
                // Activate virtual environment and install requirements
                bat 'call venv\\Scripts\\activate.bat'
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat 'call venv\\Scripts\\activate.bat'
                bat 'pytest'
            }
        }

        stage('Build Application') {
            steps {
                bat 'mkdir build'
                bat 'xcopy * build /E /I /Y'
            }
        }

        stage('Deploy Application') {
            steps {
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
