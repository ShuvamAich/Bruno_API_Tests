pipeline {
    agent any

    options {
        timestamps()
    }

    environment {
        BRUNO_ENV = 'Books Environment'
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out source from the configured SCM
                checkout scm
            }
        }

        stage('Install Bruno CLI') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm install -g @usebruno/cli'
                    } else {
                        bat 'npm install -g @usebruno/cli'
                    }
                }
            }
        }

        stage('Run Bruno API Tests') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'bru run --env "Books Environment"'
                    } else {
                        bat 'bru run --env "Books Environment"'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Bruno API tests passed.'
        }
        failure {
            echo 'Bruno API tests failed.'
        }
    }
}
