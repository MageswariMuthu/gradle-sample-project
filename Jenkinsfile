pipeline {
    agent any

    tools {
        jdk 'java'      // Ensure Java is configured in Jenkins
        gradle 'gradle' // Ensure Gradle is configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/MageswariMuthu/gradle-sample-project.git', branch: 'main'
            }
        }

        stage('Gradle Build') {
            steps {
                sh 'gradle clean build'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'app/build/libs/*.jar', fingerprint: true
            }
        }

        stage('Run Application') {
            steps {
                sh 'java -jar app/build/libs/*.jar'
            }
        }
    }
}
