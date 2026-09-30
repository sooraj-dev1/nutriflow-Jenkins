pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out NutriFlow source code...'
                checkout scm
            }
        }

        stage('Backend - Install') {
            steps {
                echo 'Installing backend dependencies...'
                dir('backend') {
                    sh 'npm ci'
                }
            }
        }

        stage('Backend - Test') {
            steps {
                echo 'Running backend tests...'
                dir('backend') {
                    sh 'npm test'
                }
            }
        }

        stage('Backend - Build') {
            steps {
                echo 'Building backend...'
                dir('backend') {
                    sh 'npm run build --if-present'
                }
            }
        }

        stage('Frontend - Install') {
            steps {
                echo 'Installing frontend dependencies...'
                dir('frontend') {
                    sh 'npm ci'
                }
            }
        }

        stage('Frontend - Test') {
            steps {
                echo 'Running frontend tests...'
                dir('frontend') {
                    sh 'npm test'
                }
            }
        }

        stage('Frontend - Build') {
            steps {
                echo 'Building frontend...'
                dir('frontend') {
                    sh 'npm run build'
                }
            }
        }
    }

    post {
        success {
            echo '======================================'
            echo 'NutriFlow CI Pipeline Successful!'
            echo 'Install, Test and Build completed.'
            echo '======================================'
        }

        failure {
            echo '======================================'
            echo 'NutriFlow CI Pipeline Failed!'
            echo 'Check the failed stage in Jenkins.'
            echo '======================================'
        }

        always {
            echo 'Jenkins pipeline execution completed.'
        }
    }
}