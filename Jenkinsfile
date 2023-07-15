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
    stage('sonar code analysis') {
      steps {
      // need to integrate the sonar
        withSonarQubeEnv("SonarQube"){
            bat "mvn sonar:sonar"
        }
      }
    }
  }
}
