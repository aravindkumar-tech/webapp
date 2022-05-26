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
    
   stage ('Build') {
      steps {
      sh 'mvn clean package'
      }
   }
    
   stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@18.169.238.90:/prod/apache-tomcat-9.0.63/webapps/webapp.war'
              }      
           }       
    }
    
  }
}
 
