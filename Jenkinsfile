pipeline {
    agent any

    tools {
        nodejs "NodeJS-22"   // configured in Jenkins
    }

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                bat 'node -v'       // Check Node.js version
                bat 'npm -v'        // Check npm version
                bat 'npm install'   // Install project dependencies
            }
        }
        stage('Test') {
            steps {
                echo '✅ Skipping snyk test for now...'
                // bat 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add your deploy command here
                // bat 'npm run deploy'
            }
        }
    }

    post {
        success {
            mail to: 'khalidalotaibi011@gmail.com',
                 subject: "SUCCESS: Jenkins Build ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The Jenkins build for ${env.JOB_NAME} completed successfully.\nCheck console output at ${env.BUILD_URL}"
        }
        failure {
            mail to: 'khalidalotaibi011@gmail.com',
                 subject: "FAILURE: Jenkins Build ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The Jenkins build for ${env.JOB_NAME} failed.\nCheck console output at ${env.BUILD_URL}"
        }
    }
}
