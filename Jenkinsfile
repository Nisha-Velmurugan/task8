pipeline {
    agent any

    environment {
        PYTHON_HOME = '/usr/bin/python3'  
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Nisha-Velmurugan/task8.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'python3 -m venv venv'
                    sh 'source venv/bin/activate'
                    sh 'pip install -r requirements.txt'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'source venv/bin/activate && pytest --cov=app --junitxml=report.xml'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('SonarQube') {
                        sh 'source venv/bin/activate && sonar-scanner'
                    }
                }
            }
        }
    }
}
