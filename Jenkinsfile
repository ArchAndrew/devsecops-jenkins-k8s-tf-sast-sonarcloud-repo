pipeline {
  agent any
  tools { 
        maven 'Maven_3.8.4'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=archandrew_sonartest -Dsonar.organization=andrew -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=ea8ff63f8f6f6bc83b633e39b3a1d70ca537b666'
			}
        } 
  }
}
