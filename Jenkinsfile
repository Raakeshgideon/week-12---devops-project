pipeline {
    agent any

    stages {

        stage('Install & Test') {
            steps {
               bat 'python -m pip install -r requirements.txt'
               bat 'python -m pytest'

            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat '''
                    sonar-scanner \
                    -Dsonar.projectKey=week12-devops \
                    -Dsonar.sources=.
                    '''
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t yourdockerhub/week12-devops .'
            }
        }
    }
}
