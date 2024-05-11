pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                git branch: 'main', url: 'https://github.com/PranavGoyal69/Task-6.1p-sit223.git'
            }
        }
        
        stages {
        stage('Build') {
            steps {
                // Build the code using Maven
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                // Run unit tests using JUnit and integration tests using a tool like Selenium
                sh 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
                // Integrate SonarQube for code analysis
                script {
                    def scannerHome = tool 'SonarQubeScanner'
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                // Perform security scan using OWASP ZAP
                sh 'zap-full-scan.py -t http://your_application_url'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                // Deploy application to staging server (e.g., AWS EC2 instance)
                sh 'ssh user@staging-server "deploy_script.sh"'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests on staging environment
                sh 'run_integration_tests.sh'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                // Deploy application to production server (e.g., AWS EC2 instance)
                sh 'ssh user@production-server "deploy_script.sh"'
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
