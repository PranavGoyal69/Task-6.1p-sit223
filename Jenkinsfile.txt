pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Build the code using Maven
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                // Run unit tests using JUnit
                sh 'mvn test'
                
                // Run integration tests using tools like Selenium, JUnit, etc.
                // Command to execute integration tests
            }
        }
        
        stage('Code Analysis') {
            steps {
                // Integrate a code analysis tool (e.g., SonarQube)
                // Command to run code analysis
            }
        }
        
        stage('Security Scan') {
            steps {
                // Perform security scan using a tool (e.g., OWASP ZAP)
                // Command to run security scan
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                // Deploy application to staging server (e.g., AWS EC2 instance)
                // Command to deploy to staging
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests on staging environment
                // Command to execute integration tests on staging
            }
        }
        
        stage('Deploy to Production') {
            steps {
                // Deploy application to production server (e.g., AWS EC2 instance)
                // Command to deploy to production
            }
        }
    }
    
    post {
        success {
            // Send notification email upon successful completion
            emailext (
                to: 'gpranav2901@gmail.com',
                subject: "Pipeline Status: SUCCESS",
                body: "Pipeline completed successfully.",
                attachmentsPattern: '**/*.log'
            )
        }
        failure {
            // Send notification email upon failure
            emailext (
                to: 'gpranav2901@gmail.com',
                subject: "Pipeline Status: FAILURE",
                body: "Pipeline failed. Please check logs for details.",
                attachmentsPattern: '**/*.log'
            )
        }
    }
}
