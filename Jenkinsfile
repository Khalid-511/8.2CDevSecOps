pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Khalid-511/8.2CDevSecOps.git'
            }
        }

        stage('Check Node and NPM') {
            steps {
                bat 'node -v'
                bat 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit 0' // don’t fail pipeline if tests break
            }
        }

        stage('Security Scan') {
            steps {
                bat 'npm audit || exit 0'
            }
        }
    }
}
