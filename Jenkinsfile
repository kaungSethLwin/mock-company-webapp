pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh './gradlew assemble'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh './gradlew test'
            }
        }
    }

    post {
        always {
            // Archive the test results
            junit '**/build/test-results/test/*.xml'
            // Archive the build artifacts
            archiveArtifacts artifacts: '**/build/libs/*.jar', allowEmptyArchive: true
        }
        failure {
            // Notify on failure (e.g., send an email, Slack notification, etc.)
            echo 'Build or tests failed.'
        }
        success {
            echo 'Build and tests succeeded.'
        }
    }
}
