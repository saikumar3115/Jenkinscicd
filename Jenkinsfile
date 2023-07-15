pipeline {
  agent  none
  tools{
    maven "MAVEN_HOME"
  }
  stages {
    stage('Get the code') {
      steps {
        git branch: 'main', url: 'https://github.com/saikumar3115/Jenkinscicd.git'
      }
    }
    stage('compile the code') {
      steps {
        // build the project and create a JAR file
        bat "mvn compile"
      }
    }
    stage('Build the code') {
      steps {
        // build the project and create a JAR file
        bat "mvn clean package"
      }
    }
  }
}
