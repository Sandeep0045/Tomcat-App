node{
   stage('SCM checkout'){
     git 'https://github.com/Sandeep0045/Tomcat-App.git'
   }
   
   
  stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'maven-3', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"

  }

   
   stage('Deploy to Nexus'){
      steps{
            nexusArtifactUploader artifacts: [
                [
                    artifactId: 'Tomcat-App', 
                    classifier: '', 
                    file: 'target/myweb-0.0.5.war', 
                    type: 'war'
               ]
            ], 
            credentialsId: 'nexus3', 
            groupId: 'in.javahome', 
            nexusUrl: '172.31.77.32:8081', 
            nexusVersion: 'nexus3', 
            protocol: 'http', 
            repository: 'tomcat-release-app', 
            version: '0.0.5'
      }
   }  
  
  
  stage('Deploy to Tomcat'){
      
     sshagent(['infra-dev']) {
        sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@172.31.87.139:/opt/tomcat/webapps/'
     }
  }
}
