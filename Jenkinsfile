pipeline {
    agent any

    stages {
        stage('Test Webhook') {
            steps {
                echo "GitHub webhook triggered successfully!"
                sh 'date'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'sonar-scanner -Dsonar.projectKey=appolo-project -Dsonar.sources=.'
                }
            }
        }
    }
}
