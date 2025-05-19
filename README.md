# A Simple Maven App
A basic Java project using Maven and JUnit 5 to demonstrate building and testing with Jenkins.

## 📦 Project Structure

```bash
simple-maven-app/
├── pom.xml
└── src/
├── main/
│ └── java/com/example/App.java
└── test/
└── java/com/example/AppTest.java
```

## 🚀 Features

- Java 11 application
- Built with Maven
- Unit tests with JUnit 5
- Jenkins pipeline support

## 🛠️ Prerequisites

- Java 11+
- Maven 3.6+
- (Optional) Jenkins for CI/CD

## 🧪 Run Locally

Clone the repo and run:
```bash
git clone https://github.com/your-username/simple-maven-app.git
cd simple-maven-app
```
Build and test:
```bash
mvn clean install
```
Run the app:
```bash
java -cp target/simple-maven-app-1.0-SNAPSHOT.jar org.example.App
```
🧪 Testing
To run unit tests:
```bash
mvn test
```

🤖 Jenkins Integration
A sample Jenkins pipeline (Jenkinsfile) is included. The pipeline:

- Checks out the code

- Compiles the source code

- Runs tests using Maven Surefire

- Packages the application

Example Jenkins Pipeline
```bash
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
```

📬 Contact
Created by Satya – feel free to reach out!
