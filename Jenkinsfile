pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Define steps for checking out your source code from your SCM system here
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Define steps for building your project here
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Define steps for running tests here
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Define steps for running SonarQube analysis here
                script {
                    def scannerHome = tool 'SonarQubeScanner'
                    withSonarQubeEnv('SonarQube_Server_Name') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                // Define steps for deploying your project here
                sh 'mvn deploy'
            }
        }
    }

    post {
        always {
            // Add any post-build actions or notifications here
        }
    }
}
