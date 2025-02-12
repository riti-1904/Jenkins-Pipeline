pipeline {
    agent {
        docker {
            image 'openjdk:11'
        }
    }

    environment {
        ENVIRONMENT = 'development' // Change to 'production' if needed
    }

    stages {
        stage('Check Environment') {
            steps {
                script {
                    if (env.ENVIRONMENT == 'production') {
                        echo 'This is a Production Build'
                    } else {
                        echo 'This is a Development Build'
                    }
                }
            }
        }

        stage('Parallel Execution') {
            parallel {
                stage('Compile Task 1') {
                    steps {
                        sh 'javac Task1.java'
                    }
                }
                stage('Compile Task 2') {
                    steps {
                        sh 'javac Task2.java'
                    }
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.class', fingerprint: true
            }
        }

        stage('Cleanup Workspace') {
            steps {
                cleanWs()
            }
        }
    }
}
