pipeline {
  agent any

  triggers {
    pollSCM('* * * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/sonjw3/new-repo.git'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTest=true'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Deploy') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat-manager', url: 'http://192.168.56.101:8080')], contextPath: null, war: 'target/hello-wordl.war'
      }
    }
  }
}

