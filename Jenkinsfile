pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Pulling code from GitHub...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests with Pytest') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest --maxfail=1 --disable-warnings -q
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Tests passed!'
        }
        failure {
            echo '❌ Tests failed!'
        }
    }
}
