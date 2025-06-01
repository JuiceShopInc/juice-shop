pipeline {
    agent any
    
    options {
        disableConcurrentBuilds()
    }

    stages {        
        stage('Build') { 
            steps {
                sh 'cat cycode.txt' 
            }
        }
    }
}
