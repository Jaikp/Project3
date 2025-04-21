pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building project with Gradle...'
                sh './gradlew clean build'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh './gradlew test'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo 'Archiving build artifacts...'
                archiveArtifacts artifacts: '**/build/libs/*.jar', fingerprint: true
                junit '**/build/test-results/test/*.xml'
            }
        }
    }

    post {
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed. Please check the logs.'
        }
    }
}
