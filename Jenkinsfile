pipeline {
    agent any

    environment {
        Repository = '8.1CDevSecOp'
        EMAIL_RECIPIENT = 'keyurpipaliya4597@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    try {
                        echo 'Running unit and integration tests...'
                        currentBuild.description = 'Tests Passed'
                    } catch (e) {
                        currentBuild.description = 'Tests Failed'
                        throw e
                    }
                }
            }
            post {
                success {
                    emailext(
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "SUCCESS: Unit and Integration Tests",
                        body: "The Unit and Integration Tests stage completed successfully.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "FAILURE: Unit and Integration Tests ",
                        body: "The Unit and Integration Tests stage failed.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running static code analysis...'
            }
        }

        stage('Security Scans') {
            steps {
                script {
                    try {
                        echo 'Performing security scans...'
                        currentBuild.description = 'Security Scan Passed'
                    } catch (e) {
                        currentBuild.description = 'Security Scan Failed'
                        throw e
                    }
                }
            }
            post {
                success {
                    emailext(
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "SUCCESS: Security Scans",
                        body: "The Security Scans stage completed successfully.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "FAILURE: Security Scans",
                        body: "The Security Scans stage failed.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
            }
        }

        stage('Integration Testing on Staging') {
            steps {
                echo 'Running integration tests on staging...'
            }
        }

        stage('Deploy to Production') {
            steps {
                input message: 'Approve deployment to production?', ok: 'Deploy'
                echo 'Deploying to production environment...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
