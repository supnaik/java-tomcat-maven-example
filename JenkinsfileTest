node{
      stage('Checkout'){
         git 'https://github.com/rajnikhattarrsinha/java-tomcat-maven-example'
      }  
      stage('Build'){
         // Get maven home path and build
         def mvnHome =  tool name: 'Maven 3.5.4', type: 'maven'   
         sh "${mvnHome}/bin/mvn package"
      }
      stage ('Test'){
         def mvnHome =  tool name: 'Maven 3.5.4', type: 'maven'    
         sh "${mvnHome}/bin/mvn verify; sleep 3"
      }  
      stage('Deploy') {     
          sshagent(['abeab169-3c7e-4291-98f3-7f190a3d4099']) {            
               sh 'scp -o StrictHostKeyChecking=no target/*.war root@54.224.162.125:/opt/tomcat/webapps'         
           }
     }
      
 }
