pipeline {
    agent any
    
    environment {
        // Define your SonarQube project key as an environment variable
        SONAR_PROJECT_KEY = 'sqp_c34a7eae26b17988901f809b97d61f6ee00c681'
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
                    sh "mvn sonar:sonar -Dsonar.projectKey=${SONAR_PROJECT_KEY}"
                }
            }
        }
        
        // Add more stages for deployment or other steps as needed
    }
    
  //  post {
        always {
            node {
                // Archive build artifacts (if needed)
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }
    }
        success {
            // Send notifications or perform actions on successful build
            echo 'Build and analysis completed successfully.'
        }

        failure {
            // Send notifications or perform actions on build failure
            echo 'Build and analysis failed.'
        }//
    }

