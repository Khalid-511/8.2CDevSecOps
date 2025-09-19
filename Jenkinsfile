pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application... (Tool: Maven or npm)'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit & integration tests... (Tools: JUnit, Mocha)'
                bat 'echo Test logs > test-stage.log'
            }
            post {
                success {
                    emailext(
                        subject: "SUCCESS: Tests Stage - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: """The **Tests** stage succeeded for build ${env.BUILD_NUMBER}.  
                                 See attached logs or check Jenkins: ${env.BUILD_URL}""",
                        to: 's224206508@gmail.com',
                        attachmentsPattern: 'test-stage.log'
                    )
                }
                failure {
                    emailext(
                        subject: "FAILURE: Tests Stage - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: """The **Tests** stage failed for build ${env.BUILD_NUMBER}.  
                                 See attached logs or check Jenkins: ${env.BUILD_URL}""",
                        to: 's224206508@gmail.com',
                        attachmentsPattern: 'test-stage.log'
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analysing code quality... (Tool: SonarQube)'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scanning for vulnerabilities... (Tool: Snyk / OWASP)'
                bat 'echo Security scan logs > security-stage.log'
            }
            post {
                success {
                    emailext(
                        subject: "SUCCESS: Security Scan - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: """The **Security Scan** stage succeeded for build ${env.BUILD_NUMBER}.  
                                 See attached logs or check Jenkins: ${env.BUILD_URL}""",
                        to: 's224206508@gmail.com',
                        attachmentsPattern: 'security-stage.log'
                    )
                }
                failure {
                    emailext(
                        subject: "FAILURE: Security Scan - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: """The **Security Scan** stage failed for build ${env.BUILD_NUMBER}.  
                                 See attached logs or check Jenkins: ${env.BUILD_URL}""",
                        to: 's224206508@gmail.com',
                        attachmentsPattern: 'security-stage.log'
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment... (Tool: Jenkins to EC2/Docker)'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running staging integration tests... (Tool: Selenium/Postman)'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production... (Tool: Jenkins + AWS/Kubernetes)'
            }
        }
    }
}
