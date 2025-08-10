pipeline {
    agent any

    tools {
        nodejs 'Node24'
    }

    stages {
        stage('Test Webhook') {
            steps {
                echo "GitHub webhook triggered successfully!"
                sh 'date'
            }
        }

        stage('Build') {
            steps {
                echo "Installing dependencies and building React app..."
                sh '''
                    npm install
                    npm run build
                '''
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    withCredentials([string(credentialsId: 'Sonar-Token', variable: 'SONAR_AUTH_TOKEN')]) {
                        script {
                            def scannerHome = tool 'SonarScanner'
                            sh """
                                ${scannerHome}/bin/sonar-scanner \
                                -Dsonar.projectKey=appolo-project \
                                -Dsonar.sources=src \
                                -Dsonar.host.url=$SONAR_HOST_URL \
                                -Dsonar.login=$SONAR_AUTH_TOKEN
                            """
                        }
                    }
                }
            }
        }
    }
}
