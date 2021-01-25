pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }

    stage('Build image') {
      app = docker.build("lchomatek/jenkins-test')
    }
    
    stage('Push image') {
    	docket.withRegistry('https://registry.hub.docker.com', 'my-docker-hub-credentials') {
    	  app.push("latest")
    	}
    }
  }
}
