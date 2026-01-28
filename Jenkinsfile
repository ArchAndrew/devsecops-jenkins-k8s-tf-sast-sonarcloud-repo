pipeline {
  agent any
  tools { 
        maven 'Maven_3.8.4'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=archandrew_sonartest -Dsonar.organization=andrew -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=b309b95aeca4b0957b69c7e72e65e01562a07f94'
			}
        } 
  }
}
