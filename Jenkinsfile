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
                sh './gradlew clean build' // Using the wrapper for consistency
            }
        }
        stage('Publish JUnit Results') {
            steps {
                junit 'app/build/test-results/test/*.xml' // JUnit test results location
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'app/build/libs/*.jar', fingerprint: true
            }
        }

        stage('Run Application') {
            steps {
                script {
                    def jarFile = sh(script: "ls app/build/libs/*.jar | head -n 1", returnStdout: true).trim()
                    if (jarFile) {
                        sh "java -jar ${jarFile}"
                    } else {
                        error "No JAR file found in app/build/libs/"
                    }
                }
            }
        }
    }
}
