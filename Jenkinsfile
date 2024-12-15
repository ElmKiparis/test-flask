pipeline {
    options { 
        timestamps() 
    }

    agent none

    stages {
        stage('Check scm') {
            agent any
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
            agent { 
                docker { 
                    image 'python:3.9-alpine'
                    args '-u root'
                    reuseNode true
                } 
            }

            steps {
                sh '''
                    apk add --update python3 py3-pip
                    pip3 install Flask xmlrunner
                    python3 app_tests.py
                '''
            }
        }
    }
}
