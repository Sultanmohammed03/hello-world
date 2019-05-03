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
        sh "/opt/apache-maven-3.6.0/bin/mvn clean package"
      }
    }
    stage ('Nexus') {
      steps {
      nexusArtifactUploader artifacts: [[artifactId: 'demo', classifier: '', file: 'webapp/target/webapp.war', type: 'war']], credentialsId: 'nexus', groupId: 'Demo', nexusUrl: '54.91.35.9:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '2.${BUILD_NUMBER}'
      }
    }
     stage ('Copy to tomcat') {
      steps {
        sh "scp /var/lib/jenkins/workspace/Demo/webapp/target/webapp.war ec2-user@10.0.1.22:/home/ec2-user/Ansible/playbooks/roles/tomcat/files"
      }
    }   
  }
}
