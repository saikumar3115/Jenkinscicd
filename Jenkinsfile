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
   // stage("Quality gate") {
    //  steps {
      //waitForQualityGate abortPipeline: true
      // }
   //}
   // stage("Build docker image") {
   //   steps {
   //   	script{
   //	  bat "docker build -t saikumar3115/springboot:1 ."
	//}
   //    }
 //  }
//  stage("push docker image") {
//      steps {
   //   	script{
//	 withCredentials([string(credentialsId: 'hellodocker', variable: 'jenkinsdockerhub')]) { 
    // 		bat "docker login -u saikumar3115 -p ${docker-jenkins}"
//	}
   //	  bat "docker push saikumar3115/springboot:1 ."
//	}
    //   }
  // }

 stage('Build and Push Docker Image') {
      environment {
        DOCKER_IMAGE = "saikumar3115/springboot:${BUILD_NUMBER}"
        REGISTRY_CREDENTIALS = credentials('dockerhubcom')
      }
      steps {
        script {
            bat "cd C:\\Users\\saiku\\.jenkins\\workspace\\CICD\\target\\ && docker build -t ${DOCKER_IMAGE} ."
            def dockerImage = docker.image("${DOCKER_IMAGE}")
            docker.withRegistry('https://hub.docker.com', "dockerhubcom") {
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
