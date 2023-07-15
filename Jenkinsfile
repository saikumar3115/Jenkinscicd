pipeline {
  agent  any
  tools{
    maven "MAVEN_HOME"
  }
  stages {
    stage('Get the code, compile , and build') {
      steps {
        git branch: 'main', url: 'https://github.com/saikumar3115/Jenkinscicd.git'
        bat "mvn compile"
        bat "mvn clean package"
      }
    }
    stage('SonarQube analysis') {
      steps {
		// Change this as per your Jenkins Configuration
        withSonarQubeEnv('SonarQube') {
                    bat 'mvn package sonar:sonar'
        }
      }
    }
  }
}
