pipeline {
    agent any

    environment {
        VIRTUAL_ENV = 'venv'
    }

    stages {
        stage('Setup') {
            steps {
                script {
                    echo "Setting up Python virtual environment..."
                    if (isUnix()) {
                        sh """
                            if [ ! -d "${VIRTUAL_ENV}" ]; then
                                python3 -m venv ${VIRTUAL_ENV}
                            fi
                            . ${VIRTUAL_ENV}/bin/activate
                            pip install -r requirements.txt
                        """
                    } else {
                        bat """
                            if not exist ${VIRTUAL_ENV} (
                                python -m venv ${VIRTUAL_ENV}
                            )
                            ${VIRTUAL_ENV}\\Scripts\\pip install -r requirements.txt
                        """
                    }
                }
            }
        }

        stage('Lint') {
            steps {
                script {
                    echo "Running flake8 linter..."
                    if (isUnix()) {
                        sh """
                            . ${VIRTUAL_ENV}/bin/activate
                            flake8 app.py --max-line-length=120
                        """
                    } else {
                        bat """
                            ${VIRTUAL_ENV}\\Scripts\\flake8 app.py --max-line-length=120
                        """
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo "Running unit tests with pytest..."
                    if (isUnix()) {
                        sh """
                            . ${VIRTUAL_ENV}/bin/activate
                            pytest tests/ -v
                        """
                    } else {
                        bat """
                            ${VIRTUAL_ENV}\\Scripts\\pytest tests/ -v
                        """
                    }
                }
            }
        }

        stage('Coverage') {
            steps {
                script {
                    echo "Running code coverage analysis..."
                    if (isUnix()) {
                        sh """
                            . ${VIRTUAL_ENV}/bin/activate
                            coverage run -m pytest tests/
                            coverage report -m
                            coverage html
                        """
                    } else {
                        bat """
                            ${VIRTUAL_ENV}\\Scripts\\coverage run -m pytest tests/
                            ${VIRTUAL_ENV}\\Scripts\\coverage report -m
                            ${VIRTUAL_ENV}\\Scripts\\coverage html
                        """
                    }
                }
            }
            post {
                always {
                    publishHTML(target: [
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'htmlcov',
                        reportFiles: 'index.html',
                        reportName: 'Coverage Report'
                    ])
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo "Running security scan with bandit..."
                    if (isUnix()) {
                        sh """
                            . ${VIRTUAL_ENV}/bin/activate
                            bandit -r . -f txt -o bandit-report.txt || true
                            cat bandit-report.txt
                        """
                    } else {
                        bat """
                            ${VIRTUAL_ENV}\\Scripts\\bandit -r . -f txt -o bandit-report.txt || exit 0
                            type bandit-report.txt
                        """
                    }
                }
            }
            post {
                always {
                    archiveArtifacts artifacts: 'bandit-report.txt', allowEmptyArchive: true
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying application..."
                    echo "Student: Hassan Khalil"
                    echo "ID: 202300935"
                    echo "Deployment successful - Application is ready!"

                    if (isUnix()) {
                        sh """
                            echo "Deployment Info" > deployment-info.txt
                            echo "Student: Hassan Khalil" >> deployment-info.txt
                            echo "ID: 202300935" >> deployment-info.txt
                            echo "Deployment Time: \$(date)" >> deployment-info.txt
                            echo "Application deployed successfully!" >> deployment-info.txt
                        """
                    } else {
                        bat """
                            echo Deployment Info > deployment-info.txt
                            echo Student: Hassan Khalil >> deployment-info.txt
                            echo ID: 202300935 >> deployment-info.txt
                            echo Deployment Time: %date% %time% >> deployment-info.txt
                            echo Application deployed successfully! >> deployment-info.txt
                        """
                    }
                }
            }
            post {
                success {
                    archiveArtifacts artifacts: 'deployment-info.txt', allowEmptyArchive: true
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed!"
            echo "Build Status: ${currentBuild.result}"
        }
        success {
            echo "All stages passed successfully!"
        }
        failure {
            echo "Pipeline failed. Please check the logs."
        }
    }
}
