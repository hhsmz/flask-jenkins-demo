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
                bat 'python -m venv venv'
                bat 'venv\\Scripts\\activate && pip install -r requirements.txt'
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat 'venv\\Scripts\\activate && pytest'
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
}
