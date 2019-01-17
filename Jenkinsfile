node{
      
      stage('SCM Checkout'){
         git 'https://github.com/rajnikhattarrsinha/java-tomcat-maven-example'
      }
  
      stage('Mvn Build'){
         // Get maven home path and build
         def mvnHome =  tool name: 'Maven 3.5.4', type: 'maven'   
         sh "${mvnHome}/bin/mvn package"
      }
      
     stage ('Test'){
         def mvnHome =  tool name: 'Maven 3.5.4', type: 'maven'    
         sh "${mvnHome}/bin/mvn verify; sleep 3"
      }  
      
    stage('Build Docker Image'){
         sh 'docker build -t rajnikhattarrsinha/docker1701:2.0.0 .'
      }  
   
      stage('Publish Docker Image'){
         withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerPWD')]) {
              sh "docker login -u rajnikhattarrsinha -p ${dockerPWD}"
         }
        sh 'docker push rajnikhattarrsinha/docker1701:2.0.0'
      }

      // stage('Stop running containers'){        
      // def scriptRunner='sudo ./stopscript.sh'
      // sshagent(['tomcatdeploymentserver']) {             
             // sh "ssh -o StrictHostKeyChecking=no rajni@35.196.19.161 ${scriptRunner}"            
      //   }
    // } 
  
   stage('Pull Docker Image and Deploy'){            
            def dockerContainerName = 'docker-$JOB_NAME-$BUILD_NUMBER'
            def dockerRun= "sudo docker run -p 8080:9091 -d --name ${dockerContainerName} rajnikhattarrsinha/docker1701:2.0.0"         
               sshagent(['tomcatdeploymentserver']) {   
               sh "ssh -o StrictHostKeyChecking=no rajni@35.196.19.161 ${dockerRun}"
             }
      }
 }


