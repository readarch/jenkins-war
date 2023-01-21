pipeline {
   agent any

   def tomcatWeb = '/Users/renzo.araos/Globant/03-Servers/apache-tomcat-10.0.27/webapps'
   def tomcatBin = '/Users/renzo.araos/Globant/03-Servers/apache-tomcat-10.0.27/bin'

   stage('SCM Checkout ...') {
      git 'https://github.com/readarch/jenkins-war.git'
   }

   stage('Compile, Package, Create War File ...') {
      // Get maven home path
      def mvnHome =  tool name: 'mvn-3.8.7', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }

   stage('Deploy to Tomcat ...') {
      sh "cp /target/JenkinsWar.war ${tomcatWeb}/JenkinsWar.war"
   }

   stage('Start Tomcat Server ...') {
      sleep(time:5,unit:"SECONDS") 
      sh "${tomcatBin}/startup.sh"
      sleep(time:100,unit:"SECONDS")
   }
}
