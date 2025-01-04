pipeline {
    agent any

    environment {
        PYTHON_HOME = '/usr/bin/python3'  
        SONARQUBE_HOST = 'http://localhost:9000'  
        SONARQUBE_TOKEN = 'sqp_41f3361f9e0069074a002dc1fe266fe857e0f29c' 
        SONAR_PROJECT_KEY = 'task8'  
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
                    sh """
                    source venv/bin/activate
                    sonar-scanner \
                        -Dsonar.projectKey=${env.SONAR_PROJECT_KEY} \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=${env.SONARQUBE_HOST} \
                        -Dsonar.token=${env.SONARQUBE_TOKEN}
                    """
                }
            }
        }
    }
}
