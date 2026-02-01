pipeline {
    agent any

    environment {
        PYTHON_EXE = 'C:\\Users\\raake\\AppData\\Local\\Programs\\Python\\Python311\\python.exe'
        SONAR_SCANNER = 'C:\\Program Files\\sonarQube\\sonar-scanner\\sonar-scanner-8.0.1.6346-windows-x64\\bin\\sonar-scanner.bat'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install & Test') {
            steps {
                bat """
                "${PYTHON_EXE}" -m pip install --upgrade pip
                "${PYTHON_EXE}" -m pip install -r requirements.txt
                "${PYTHON_EXE}" -m pytest
                """
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('week 12 - devops') {
                    bat """
                    "${SONAR_SCANNER}" ^
                    -Dsonar.projectKey=week12-devops ^
                    -Dsonar.projectName=week12-devops ^
                    -Dsonar.sources=. ^
                    -Dsonar.host.url=http://localhost:9000
                    """
                }
            }
        }

        stage('Quality Gate') {
            steps {
                echo 'Skipping Quality Gate for local Jenkins demo'
            }
        }

        stage('Docker
