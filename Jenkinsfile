//Jenkins pipeline script
//Groovy script 

node()
  {
   def mavenHome = tool name: 'maven3.8.4'    
  stage('1.git clone')
  {
  git branch: 'dev', url: 'https://github.com/itoroukpe/maven-web-apps'
  }
  stage('2.maven-Build')
  { 
    sh "${mavenHome}/bin/mvn clean package"     
  }
  stage('3.CodeQualityReport')
  {
  sh "${mavenHome}/bin/mvn sonar:sonar"
  }
 stage('4.UploadWarNexus')
        {
        //sh "${mavenHome}/bin/mvn clean deploy"
        }
 stage('5.DeployTomcat')
        {
        deploy adapters: [tomcat9(credentialsId: '4d77fa4c-4713-4738-b0f5-ee7b58ba3b19', path: '', url: 'http://54.69.135.72:8080/')], contextPath: null, war: 'target/*war'
        }  
stage('6.approval')
        {
        timeout(time:8, unit: 'HOURS'){
            input message: 'please approve deployment to production'
        }
        }  
 stage('7.DeploytoProd')
        {
        deploy adapters: [tomcat9(credentialsId: '4d77fa4c-4713-4738-b0f5-ee7b58ba3b19', path: '', url: 'http://54.69.135.72:8080/')], contextPath: null, war: 'target/*war'
        }   
stage('8.Email')//go to pipeline script and configure using email extension plugin
        {
        //----generate pipeline syntax and paste here
        }      
  } 
  
