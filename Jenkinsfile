pipeline {
    agent {
        docker {
            image 'openjdk:11' // Use OpenJDK 11 Docker image
        }
    }
    environment {
        APP_ENV = "development"  // Change to "production" if needed
        APP_VERSION = "1.0"
    }
    stages {
        stage('Environment Check') {
            steps {
                script {
                    if (env.APP_ENV == 'production') {
                        echo "Production build is running..."
                    } else {
                        echo "Development build is running..."
                    }
                }
            }
        }
        
        stage('Parallel Execution') {
            parallel {
                stage('Task 1 - Compile Java Program') {
                    steps {
                        script {
                            writeFile file: 'Task1.java', text: '''
                                public class Task1 {
                                    public static void main(String[] args) {
                                        System.out.println("Hello Jenkins from Task 1.");
                                    }
                                }
                            '''
                            sh 'javac Task1.java'
                        }
                    }
                }
                stage('Task 2 - Compile Java Program') {
                    steps {
                        script {
                            writeFile file: 'Task2.java', text: '''
                                public class Task2 {
                                    public static void main(String[] args) {
                                        System.out.println("Hello Jenkins from Task 2.");
                                    }
                                }
                            '''
                            sh 'javac Task2.java'
                        }
                    }
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '*.class', fingerprint: true
            }
        }

        stage('Workspace Cleanup') {
            steps {
                cleanWs()
            }
        }
    }
}
