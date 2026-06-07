pipeline {
    agent {
        docker {
            image 'maven:3.9.6-eclipse-temurin-17'
        }
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }

    post {
        always {
            junit allowEmptyResults: true,
                  testResults: '**/target/surefire-reports/*.xml'

            archiveArtifacts artifacts: 'target/**/*.jar',
                             fingerprint: true,
                             allowEmptyArchive: true
        }
    }
}