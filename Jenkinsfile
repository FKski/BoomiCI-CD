pipeline {
    agent any
    triggers {
        pollSCM '* * * * *'
    }
    environment {
        // Replace 'YourSonarQubeServer' with the name of your configured SonarQube server in Jenkins
        SONARQUBE_SERVER = 'SonarQubeServer'
        
        // SonarQube token stored as a Jenkins credential (replace 'sonarqube-token' with your credential ID)
        SONARQUBE_TOKEN = credentials('SonarQube_token')
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                python HelloWorld.py
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                echo "doing test stuff.."
                '''
            }
        }
        stage('SonarQube Analysis') {
            steps{
                script{
                    def scannerHome = tool 'SonarQube_Scanner';
                    withSonarQubeEnv() {
                    sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
    post {
        always {
            // Optional cleanup after pipeline completes
            echo "Pipeline completed."
        }
    }
}
