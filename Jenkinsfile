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

            steps {
                sh '''
                    apk add --update python3 py3-pip
                    pip3 install Flask xmlrunner
                    python3 test.py
                '''
            }
        }
    }
}
