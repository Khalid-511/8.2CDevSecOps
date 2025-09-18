pipeline {
    agent any

    tools {
        nodejs "NodeJS-22"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                bat 'node -v'
                bat 'npm -v'
                bat 'npm install'
            }
        }

        stage('Test with Snyk') {
            steps {
                echo 'Running Snyk security test...'
                withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
                    bat 'snyk auth %SNYK_TOKEN%'
                    // Run test and save results
                    bat 'snyk test --json > snyk-report.json || exit 0'
                }
            }
        }

        stage('Summary') {
            steps {
                script {
                    // Read the report file
                    def report = readJSON file: 'snyk-report.json'
                    def issues = report.vulnerabilities.size()
                    echo "🔒 Found ${issues} vulnerabilities"
                    // Save summary for email
                    writeFile file: 'summary.txt', text: "Snyk found ${issues} vulnerabilities.\nSee Jenkins console or attached report."
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying (simulated)...'
                // bat 'npm run deploy'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'snyk-report.json', fingerprint: true
        }
        success {
            mail to: 'khalidalotaibi011@gmail.com',
                 subject: "SUCCESS: Build ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build passed.\n\n" + readFile('summary.txt') + "\n\nCheck full report in Jenkins."
        }
        failure {
            mail to: 'khalidalotaibi011@gmail.com',
                 subject: "FAILURE: Build ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build failed.\n\n" + readFile('summary.txt') + "\n\nCheck full report in Jenkins."
        }
    }
}
