pipeline {
  agent any
  tools { 
    maven 'Maven_3.8.4'  
  }
  stages {
    stage('Compile and SonarCloud Analysis') {
      steps {
        withCredentials([string(credentialsId: 'sonarcloud-token', variable: 'SONAR_TOKEN')]) {
          dir("${env.WORKSPACE}") {   // Ensure we are in the repo root
            sh '''
              mvn clean verify sonar:sonar \
                -Dsonar.projectKey=archandrew_sonartest \
                -Dsonar.organization=andrew \
                -Dsonar.host.url=https://sonarcloud.io \
                -Dsonar.login=$SONAR_TOKEN
            '''
          }
        }
      }
    }
  }
}

