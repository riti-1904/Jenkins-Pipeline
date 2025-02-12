pipeline {
    agent {
        docker {
            image 'openjdk:11'
            args '--user root' // Ensures correct permissions
        }
    }

    environment {
        JAVA_HOME = '/usr/local/openjdk-11'
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Compile Java Program') {
            steps {
                script {
                    sh 'javac HelloWorld.java'
                }
            }
        }

        stage('Run Java Program') {
            steps {
                script {
                    sh 'java HelloWorld'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.class', fingerprint: true
            }
        }
    }

    post {
        always {
            cleanWs() // Cleans workspace after execution
        }
    }
}
