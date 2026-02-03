pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pull source code from GitHub - gradle-demo repo [cite: 67]
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                // Use Gradle for build and test execution [cite: 68, 71]
                // Adding jacocoTestReport to ensure coverage data is ready for SonarQube 
                sh './gradlew clean test jar jacocoTestReport'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Execute the SonarQube scan after build and test 
                    withSonarQubeEnv('sonar') {
                        sh './gradlew sonar'
                    }
                }
            } // Fixed the ] to } here
        }

        stage('Archive Artifact') {
            steps {
                // Archive the generated JAR file [cite: 73, 74]
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }
}
