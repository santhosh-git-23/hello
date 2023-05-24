pipeline {
  agent any
  tools {
    maven 'maven' 
  }
  triggers {
    pollSCM '* * * * *'
  }
  stages {
    stage ('Build') {
      steps {
        sh 'mvn clean package'
        sh 'mvn install -Dmaven.plugin.validation=VERBOSE'
      }
    }
    stage ('Deploy') {
      steps {
        script {
          deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://13.51.146.212:8080/')], contextPath: '/', onFailure: false, war: '**/*.war' 
        }
      }
    }
  }
}
