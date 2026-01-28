pipeline {
    agent any

    tools { 
        maven 'Maven_3.8.4'  // Use your Jenkins Maven tool name
    }

    environment {
        SONAR_TOKEN = credentials('sonarcloud-token')  // Jenkins credential ID for your SonarCloud token
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository into the workspace
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                dir("${env.WORKSPACE}") {   // Ensure Maven runs in repo root
                    sh 'mvn clean verify'
                }
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                dir("${env.WORKSPACE}") {
                    // Construct Maven command with branch/PR detection
                    script {
                        def sonarCmd = "mvn sonar:sonar " +
                            "-Dsonar.projectKey=archandrew_sonartest " +
                            "-Dsonar.organization=andrew " +
                            "-Dsonar.host.url=https://sonarcloud.io " +
                            "-Dsonar.login=$SONAR_TOKEN"

                        // If Jenkins environment variables for PR exist, add them
                        if (env.CHANGE_ID && env.CHANGE_BRANCH && env.CHANGE_TARGET) {
                            sonarCmd += " -Dsonar.pullrequest.key=${env.CHANGE_ID}" +
                                        " -Dsonar.pullrequest.branch=${env.CHANGE_BRANCH}" +
                                        " -Dsonar.pullrequest.base=${env.CHANGE_TARGET}" +
                                        " -Dsonar.pullrequest.github.repository=ArchAndrew/devsecops-jenkins-k8s-tf-sast-sonarcloud-repo"
                        }

                        echo "Running SonarCloud Analysis..."
                        sh sonarCmd
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
    }
}


