pipeline {
    agent any
    environment {
        PYTHON = 'python3'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install dependencies') {
            steps {
                script {
                    
                    sh '''
                    if ! python3 -m pip --version; then
                        echo "pip is not installed, installing pip..."
                        curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
                        python3 get-pip.py
                    fi
                    python3 -m pip install --upgrade pip
                    python3 -m pip install -r requirements.txt
                    '''
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    sh 'pytest'
                }
            }
        }
        stage('Generate Coverage Report') {
            steps {
                script {
                    sh 'coverage run -m pytest'
                    sh 'coverage report'
                    sh 'coverage html'
                }
            }
        }
    }
}
