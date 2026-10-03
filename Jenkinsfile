pipeline {
    agent any

    environment {
        MAVEN_HOME = 'C:\\apache-maven-3.9.9'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Code is already checked out by Jenkins'
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling Java application...'

                bat '''
                    set "PATH=%MAVEN_HOME%\\bin;%PATH%"
                    mvn clean compile
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'

                bat '''
                    set "PATH=%MAVEN_HOME%\\bin;%PATH%"
                    mvn test
                '''
            }
        }

        stage('Package') {
            steps {
                echo 'Creating Spring Boot JAR...'

                bat '''
                    set "PATH=%MAVEN_HOME%\\bin;%PATH%"
                    mvn package -DskipTests
                '''
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving JAR...'

                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline failed. Check the failed stage.'
        }

        always {
            echo 'Pipeline execution completed.'
        }
    }
}