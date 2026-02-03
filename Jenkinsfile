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

        // Use credentialsId to pull the token you saved in Jenkins

        withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {

            withSonarQubeEnv('SonarQube') {

                sh "./gradlew sonar -Dsonar.login=${SONAR_TOKEN}"

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
