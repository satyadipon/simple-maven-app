pipeline {
    agent any

    environment {
        SLACK_CHANNEL = '#ci-cd' // Replace it with your Slack channel
        SLACK_CREDENTIALS_ID = 'slack-cred' // From Jenkins credential manager
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/satyadipon/simple-maven-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        success {
            slackSend(
                channel: env.SLACK_CHANNEL,
                color: 'good',
                message: "✅ Job '${env.JOB_NAME}' [#${env.BUILD_NUMBER}] succeeded. 🎉\n${env.BUILD_URL}"
            )
        }
        failure {
            slackSend(
                channel: env.SLACK_CHANNEL,
                color: 'danger',
                message: "❌ Job '${env.JOB_NAME}' [#${env.BUILD_NUMBER}] failed. 🔥\n${env.BUILD_URL}"
            )
        }
        always {
            echo 'Pipeline finished.'
        }
    }
}