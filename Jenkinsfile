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
                        tool 'Node.js 18' // Use the exact name configured in Jenkins Global Tool Configuration
                        echo 'Verifying Node.js and npm versions...'
                        sh 'node -v' // Verify Node.js is on PATH
                        sh 'npm -v'  // Verify npm is on PATH
                        echo 'Installing Bruno CLI globally...'
                        sh 'npm install -g @usebruno/cli' // Install Bruno CLI
                        echo 'Verifying Bruno CLI installation...'
                        sh 'bru --version' // Verify Bruno CLI installation
                    } else {
                        tool 'Node.js 18'
                        echo 'Installing Bruno CLI globally...'
                        bat 'npm install -g @usebruno/cli'
                    }
                }
            }
        }

        stage('Run Bruno API Tests') {
            steps {
                script {
                                        withCredentials([string(credentialsId: 'simple-books-authorization', variable: 'AUTHORIZATION_TOKEN')]) {

                                                // Overwrite the Bruno environment file with the secret injected
                                                writeFile file: 'environments/Books Environment.yml', text: """name: Books Environment
variables:
    - secret: true
        name: Authorization
        value: Bearer ${AUTHORIZATION_TOKEN}
    - name: BaseUrl
        value: https://simple-books-api.click
"""

                        if (isUnix()) {
                            echo 'Running Bruno API tests...'
                            sh 'npx bru run --env "Books Environment"'
                        } else {
                            echo 'Running Bruno API tests...'
                            bat 'npx bru run --env "Books Environment"'
                        }
                    }
                }
            }
        }
        stage('Archive Test Results') {
            steps {
                echo 'Archiving test report...'
                // Save the generated HTML report as a build artifact
                archiveArtifacts artifacts: 'results.html', fingerprint: true
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
