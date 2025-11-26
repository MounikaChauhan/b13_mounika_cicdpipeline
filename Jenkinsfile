pipeline {
    agent any

    environment {
        VENV = 'venv'
        
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'Jenkins_submission'
                    url: 'https://github.com/MounikaChauhan/b13_mounika_cicdpipeline.git'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    python3 -m venv $VENV
                    source $VENV/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                    pip install pytest
                    nohup python app.py &

                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    source $VENV/bin/activate
                    pytest --disable-warnings --maxfail=1
                '''
            }
        }
    }

    post {
        success {
            emailext (
                subject: "Jenkins Build SUCCESS: ${env.JOB_NAME}",
                body: "The build passed successfully.",
                to: "mounikachauhan.30@gmail.com"
            )
        }
        failure {
            emailext (
                subject: "Jenkins Build FAILED: ${env.JOB_NAME}",
                body: "The build failed. Please check Jenkins.",
                to: "mounikachauhan.30@gmail.com"
            )
        }
    }
}
