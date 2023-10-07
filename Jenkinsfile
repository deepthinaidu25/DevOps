pipeline {
    agent any

    environment {
        // Define your SonarQube project key and token as environment variables
        SONAR_PROJECT_KEY = 'miniproj1'
        SONAR_TOKEN = credentials('sqb_ee1dd511f80a5acd1f3144f9ceb8f68e70904794')
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your Git repository
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                // Build your project using Maven
                sh 'mvn clean install'

                // Run tests (if applicable)
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Execute SonarQube analysis using the SonarQube Scanner for Maven
                withSonarQubeEnv('SonarQube Server') {
                    sh "mvn sonar:sonar -Dsonar.projectKey=${SONAR_PROJECT_KEY} -Dsonar.login=${SONAR_TOKEN}"
                }
            }
        }

        // Add more stages for deployment or other steps as needed
    }
}

