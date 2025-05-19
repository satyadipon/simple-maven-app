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
java -cp target/simple-maven-app-1.0-SNAPSHOT.jar com.example.App
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
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/simple-maven-app.git'
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
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }
}


📬 Contact
Created by Satya – feel free to reach out!
