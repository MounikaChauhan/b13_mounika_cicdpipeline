pipeline {
    agent any

    environment {
        VENV = 'venv'
        MONGO_URI = "${MONGO_URI}"
        SECRET_KEY = "${SECRET_KEY}"
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
                    python app.py

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

        stage('Deploy to Staging') {
            when {
                expression { currentBuild.result == null }
            }
            steps {
                sh '''
                    echo "Deploying Flask app to staging server..."
                    # Example deployment:
                    # scp -r . ubuntu@staging-server:/var/www/flaskapp
                '''
            }
        }
    }

    post {
        success {
            emailext (
                subject: "Jenkins Build SUCCESS: ${env.JOB_NAME}",
                body: "The build passed successfully.",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
            )
        }
        failure {
            emailext (
                subject: "Jenkins Build FAILED: ${env.JOB_NAME}",
                body: "The build failed. Please check Jenkins.",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
            )
        }
    }
}
