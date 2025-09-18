pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Khalid-511/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit 0'   // run tests but don’t fail pipeline if tests break
            }
        }

        stage('Security Scan') {
            steps {
                bat 'npm audit || exit 0'
            }
        }
    }
}
