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
	  // Need to add the sonarqube scanner and create the global token in sonar and provide it in jenkins
    stage('SonarQube analysis') {
      steps {
		// Change this as per your Jenkins Configuration
        withSonarQubeEnv('sonar') {
                    bat 'mvn package sonar:sonar'
        }
      }
    }
    stage("Quality gate") {
      steps {
      waitForQualityGate abortPipeline: true
       }
   }
    stage('Build and Push Docker Image') {
      environment {
        DOCKER_IMAGE = "saikumar3115/springboot:${BUILD_NUMBER}"
        REGISTRY_CREDENTIALS = "dockerhubcom"
	dockerImage =''
      }
      steps {
        script { 
            dockerImage = docker.build DOCKER_IMAGE
            docker.withRegistry('https://index.docker.io/v1/', REGISTRY_CREDENTIALS) {
            dockerImage.push()
            }
        }
      }
    }
  }
  post {  
    success {
      echo 'This will run only if successful'
    }
    failure {
      echo 'This will run only if failed'
    }
    
  }
}
