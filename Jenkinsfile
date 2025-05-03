pipeline {
    agent any
    environment {        
        PYTHON_VERSION = 'python3'
    }
    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install dependencies') {
            steps {
                script {
                    sh '''
                        python3 -m pip --version || echo "pip not installed"
                        if ! python3 -m pip --version > /dev/null 2>&1; then
                            echo "pip is not installed, installing pip..."
                            curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
                            python3 get-pip.py
                            python3 -m pip install --upgrade pip
                        fi
                        python3 -m pip install -r requirements.txt
                    '''
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {                    
                    sh 'export PYTHONPATH=$PYTHONPATH:$WORKSPACE/app && pytest'
                }
            }
        }
        stage('Generate Coverage Report') {
            steps {
                script {                    
                    sh 'coverage run -m pytest'
                    sh 'coverage report'
                }
            }
        }
    }
}
