pipeline {
    agent any 
    tools {
        maven 'maven'
        }
    options {
  buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
}
    stages {
        stage('Clone') { 
            steps {
                sh "rm -rf MavenProject"
                sh "git clone https://github.com/Bhavyasreethakur/MavenProject.git"
                sh "mvn clean"
            }
        }
        stage('Test') {
            steps {
               sh "mvn test" 
            }
        }
        stage('Deploy'){
            steps{
              sh "mvn package"  
            }
        }
        stage('Upload Jar to Nexus'){
            steps{
                script{
                def mavenpom = readMavenPom file: 'pom.xml'
                def nexusreponame = mavenpom.version.endsWith("SNAPSHOT") ? "samplesnapshot" : "samplerepo"
            nexusArtifactUploader artifacts: [
                [
                    artifactId: 'my-app', 
                    classifier: '', 
                    file: "target/my-app-${mavenpom.version}.jar", 
                    type: 'jar'
                ]
            ], 
                credentialsId: 'nexuscredentials', 
                groupId: 'com.mycompany.app', 
                nexusUrl: '172.31.37.196:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: nexusreponame, 
                version: "${mavenpom.version}"
                }}
        }
    }
    }
