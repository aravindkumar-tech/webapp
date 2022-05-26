pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
 
    stage ('SAST') {
      steps {
        withSonarQubeEnv('devsecops') {
          sh 'mvn sonar:sonar'
          sh 'cat target/sonar/report-task.txt'
        }
      }
    }
    
   stage ('Build') {
      steps {
      sh 'mvn clean package'
      }
   }
    
   stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@18.134.15.215:/prod/apache-tomcat-9.0.63/webapps/webapp.war'
              }      
           }       
    }
    
  }
}
 
