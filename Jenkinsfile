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
        		script {
            			withSonarQubeEnv('sonar') {
                			sh './gradlew sonar'
           			 }
       			 }
   		 }
	]

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }
}
