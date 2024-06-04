pipeline {
    agent any

    environment {
        RECIPIENT = 'rishwho120@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Using Maven to compile and package the code.'
                echo 'Tool: Maven'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests - Running unit tests to ensure code functions as expected and integration tests to ensure components work together.'
                echo 'Tools: JUnit for unit tests, TestNG for integration tests'
            }
            post {
                success {
                    script {
                        emailext (
                            subject: "Pipeline Success: Unit and Integration Tests",
                            body: "The Unit and Integration Tests stage completed successfully.",
                            recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                            to: "$RECIPIENT",
                            attachLog: true
                        )
                    }
                }
                failure {
                    script {
                        emailext (
                            subject: "Pipeline Failed: Unit and Integration Tests",
                            body: "The Unit and Integration Tests stage failed. Please check the logs.",
                            recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                            to: "$RECIPIENT",
                            attachLog: true
                        )
                    }
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis - Analyzing code to ensure it meets industry standards.'
                echo 'Tool: SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Performing a security scan to identify vulnerabilities.'
                echo 'Tool: OWASP ZAP'
            }
            post {
                success {
                    script {
                        emailext (
                            subject: "Pipeline Success: Security Scan",
                            body: "The Security Scan stage completed successfully.",
                            recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                            to: "$RECIPIENT",
                            attachLog: true
                        )
                    }
                }
                failure {
                    script {
                        emailext (
                            subject: "Pipeline Failed: Security Scan",
                            body: "The Security Scan stage failed. Please check the logs.",
                            recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                            to: "$RECIPIENT",
                            attachLog: true
                        )
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging - Deploying the application to a staging server.'
                echo 'Tool: AWS CLI'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - Running integration tests on the staging environment to ensure the application functions as expected.'
                echo 'Tool: Selenium'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - Deploying the application to a production server.'
                echo 'Tool: AWS CLI'
            }
        }
    }

    post {
        success {
            mail to: "$RECIPIENT",
                 subject: "Pipeline Success",
                 body: "The pipeline has completed successfully."
        }
        failure {
            mail to: "$RECIPIENT",
                 subject: "Pipeline Failed",
                 body: "The pipeline has failed. Please check the logs."
        }
    }
}
