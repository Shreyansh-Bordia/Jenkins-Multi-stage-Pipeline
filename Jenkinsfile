pipeline {
    agent any

    environment {
        VENV_DIR = 'venv'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                script {
                    // Create a virtual environment
                    sh 'python3 -m venv $VENV_DIR'

                    // Activate the virtual environment and install dependencies
                    sh '. $VENV_DIR/bin/activate && pip install -r requirements.txt'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                script {
                    // Activate the virtual environment and run tests
                    sh '. $VENV_DIR/bin/activate && python -m unittest discover -s .'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh '''
                mkdir -p /tmp/python-app-deploy
                cp app.py /tmp/python-app-deploy/
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for more details.'
        }
    }
}

