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
            steps {
                script {
                    echo "Running SonarQube Analysis"
                    
                    withSonarQubeEnv(SONARQUBE_SERVER) {
                        sh '''
                            sonar-scanner \
                                -Dsonar.projectKey=your_project_key \
                                -Dsonar.sources=. \
                                -Dsonar.host.url=$SONAR_HOST_URL \
                                -Dsonar.login=$SONARQUBE_TOKEN
                        '''
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
