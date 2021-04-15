node{
   stage('SCM checkout'){
     git 'https://github.com/Sandeep0045/simple-java-app.git'
   }
   
   
  stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'maven-3', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"

  }


  stage('Deploy to Tomcat'){
      
     sshagent(['infra-dev']) {
        sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@172.31.87.139:/opt/tomcat/webapps/'
     }
  }
}
