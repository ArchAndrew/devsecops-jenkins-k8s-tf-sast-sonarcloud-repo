pipeline {
  agent any
  tools { 
        maven 'Maven_3.8.4'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=archandrew_sonartest -Dsonar.organization=andrew -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=2ffadc6793d6c8f3d171b919beeaeeef2cbc08ef'
			}
        } 
  }
}
