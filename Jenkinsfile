pipeline {
    agent any

    tools {
        // These names must match the 'Name' you gave your tools in 
        // Jenkins -> Manage Jenkins -> Global Tool Configuration
        maven 'local_maven' 
        jdk   'java17'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                // This checks out the source code from the Git repository 
                // configured in the Jenkins Job
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Run Maven clean and package
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh 'mvn test'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
            // Archive the artifacts (e.g., jar/war files)
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        failure {
            echo 'Pipeline failed. Check the logs.'
        }
    }
}
