node ('master')
 {
  
  def mavenHome = tool name: "maven"
  
      echo "GitHub BranhName ${env.BRANCH_NAME}"
      echo "Jenkins Job Number ${env.BUILD_NUMBER}"
      echo "Jenkins Node Name ${env.NODE_NAME}"
  
      echo "Jenkins Home ${env.JENKINS_HOME}"
      echo "Jenkins URL ${env.JENKINS_URL}"
      echo "JOB Name ${env.JOB_NAME}"
  
   //properties([[$class: 'JiraProjectProperty'], buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '2', daysToKeepStr: '', numToKeepStr: '2')), pipelineTriggers([pollSCM('* * * * *')])])
      stage('checkout')
      git credentialsId: '7731864b-7a59-4c2a-8e1a-d9cd809cda62', url: 'https://github.com/Ayyappa376/maven-web-application-master.git'
    stage ('Build')
      sh "${mavenHome}/bin/mvn clean package"
    stage ('Code Quality Analysis')
      sh "${mavenHome}/bin/mvn sonar:sonar"
    stage ('upload to artifactory')
      sh "${mavenHome}/bin/mvn deploy"   
    stage ('Deploy to tomcat')
    {
   sshagent(['e76ed651-45a5-47d8-ae48-b8213e4015ab'])
    {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ubuntu@34.224.102.254:/opt/tomcat/apache-tomcat-9.0.53/webapps/"
    }
    }
}
