pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
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
