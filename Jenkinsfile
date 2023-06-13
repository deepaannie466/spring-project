pipeline {
 agent any
 environment {
 JAVA_HOME = tool ('JAVA_HOME')
 }
 stages {
  stage('CompileandPackage') {
   steps {
   git 'https://github.com/deepaannie466/spring-project.git'
   sh label: '', script: 'mvn clean package'
   echo "${BUILD_URL}"
   }
   }
   stage('CodeAnalysis') {
   steps {
   script {
   def scannerHome = tool 'SonarScanner';
   withSonarQubeEnv("SonarCloud") {
   sh "${tool("SonarScanner")}/bin/sonar-scanner"
   }
   }
   }
   }
   stage('DeploytoTomcat') {
   steps {
  sh label: '', script: 'cp $(pwd)/target/*.war /opt/tomcat/webapps/'
  echo "${BUILD_URL}"
   }
   }
   stage('FunctionalTesting') {
   steps {
   sleep 60
  sh label: '', script: 'mvn -Dfilename=testng-functional.xml surefire:test'
   }
   }
   }
