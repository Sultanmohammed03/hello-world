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
    stage ('Uploading - Artifact Nexus') {
      steps {
      nexusArtifactUploader artifacts: [[artifactId: 'demo', classifier: '', file: 'webapp/target/webapp.war', type: 'war']], credentialsId: 'nexus', groupId: 'Demo', nexusUrl: '54.91.35.9:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '3.${BUILD_NUMBER}'
      }
    }
         stage ('Copy webapp to Ansilbe Server') {
      steps {
        sh "scp /var/lib/jenkins/workspace/Demo/webapp/target/webapp.war ec2-user@10.0.1.22:/home/ec2-user/ansible/playbooks/roles/tomcat/files"
      }
    }
    stage ('Creating Development Server') {
      steps {
        sh "ssh ec2-user@10.0.1.22 ansible-playbook /home/ec2-user/ansible/EC2/ec2.yml"
      }
    }   
    stage ('Deploy webapp war files to Dev Server using ansible Server') {
      steps {
        sh "ssh ec2-user@10.0.1.22 ansible-playbook -i ansible/playbooks/hosts ansible/playbooks/apache-tomcat.yml"
      }
    } 
      
  }
  }
