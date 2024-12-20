pipeline {
    options {
        timestamps()
    }
    agent any

    stages {
        stage('Check SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building ...${BUILD_NUMBER}"
                echo "Build completed"
            }
        }

        stage('Test') {
            steps {
                sh 'python3 --version'
                sh 'pip --version'

                sh 'pip install Flask'
                sh 'pip install xmlrunner'
                
                sh 'python3 app_tests.py'
            }
            post {
                always {
                    junit 'test-reports/*.xml'
                }
                success {
                    echo "Application testing successfully completed"
                }
                failure {
                    echo "Oooppss!!! Tests failed!"
                }
            }
        }
    }
}
