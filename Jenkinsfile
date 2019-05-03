pipeline {
  agent any
  tools {
        maven 'Maven'
    }
  stages {
    stage ('checkout code') {
      steps {
        git 'https://github.com/Sultanmohammed03/hello-world'
      }
   }
    stage ('Run Build') {
      steps {
        sh "/opt/apache-maven-3.6.1/bin/mvn clean package"
      }
    }
  }
}
