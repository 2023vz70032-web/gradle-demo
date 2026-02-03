pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pulls the code from the Git repository defined in the job
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
               sh './gradlew clean test jar'
            }
        }

        stage('SonarQube Analysis') {
    steps {
        // Use 'sonar-token' from your screenshot
        withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_LOGIN')]) {
            withSonarQubeEnv('SonarQube') {
                // We pass the token directly to the Gradle command
                sh "./gradlew sonar -Dsonar.login=${SONAR_LOGIN}"
            }
        }
    }
}

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }
}
