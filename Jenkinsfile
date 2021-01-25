pipeline {
  agent any
  stages {
    stage('Build') {
      agent { docker { 
      	image 'maven:3-alpine'
      	args '-v /root/.m2:/root/.m2'
      	}
      }
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }

    
    stage('Push image') {
      agent { docker {
        image 'openjdk:7'
        }
      }
      steps {
        script {
    	  docker.withRegistry('', 'my-docker-hub-credentials') {
    	    def app = docker.build("lchomatek/zpu-jenkins-test")
    	    app.push("latest")
      	  }
      	}
      }
    }
  }
}
