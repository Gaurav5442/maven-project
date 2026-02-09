pipeline {
  agent any
  stages {
    stage('scm checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/Gaurav5442/maven-project.git'
      }
    }

    stage('package job') //validate compile, test and then package
    {
      steps {
        withMaven(globalMavenSettingsConfig: '', jdk: 'JDK_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
          sh 'mvn package'
        }
      }
    }

    stage('deploy job') 
    {
      steps {
      sshagent(['DEV-CICD']) {
            
        sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@3.6.160.179:/opt/tomcat/webapps'
      }
      }
    }
  }
}

// testing upstream