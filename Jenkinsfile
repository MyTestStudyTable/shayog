node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/MyTestStudyTable/shayog.git/'
      
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
            sh '"$MVN_HOME/bin/mvn" site'
           
            
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
      
   }
   //stage('Results') {
    //  junit '**/target/surefire-reports/TEST-*.xml'
     // archiveArtifacts 'target/*.jar'
   //}
   
   stage('Deployment') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            
            sh 'scp /home/vagrant/workspace/Robin/target/studyTable-0.0.1-SNAPSHOT.war  vagrant@55.55.55.58:/home/vagrant/tomcat9/webapps/studyTable.war'
            sh 'ssh vagrant@55.55.55.58 "/home/vagrant/tomcat9/bin/shutdown.sh && /home/vagrant/tomcat9/bin/startup.sh"'
         } else {
            print "copy failed"
         }
      }
      
   }
     
}
