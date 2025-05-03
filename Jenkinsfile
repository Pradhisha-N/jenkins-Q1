pipeline {
    agent any

    environment {
        PYTHON = 'python3'
    }

    stages {
        stage('Install dependencies') {
            steps {
                sh '${PYTHON} -m pip install --upgrade pip'
                sh '${PYTHON} -m pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running pytest...'
                sh 'pytest tests/'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                echo 'Generating coverage report...'
                sh 'coverage run -m pytest tests/'
                sh 'coverage report'
                sh 'coverage html'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution complete.'
        }
    }
}
