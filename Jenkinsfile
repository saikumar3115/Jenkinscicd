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
      mvn clean verify sonar:sonar \
      -Dsonar.projectKey=Jenkinscicd \
      -Dsonar.projectName='Jenkinscicd' \
      -Dsonar.host.url=http://192.168.144.1:9001/ \
      -Dsonar.token=sqp_a8a111a4aa6b2a8415baf1d8f0e2332334d6c994
        
      }
    }
  }
}
