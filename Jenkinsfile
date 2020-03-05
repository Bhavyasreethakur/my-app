pipeline {
    agent any 
    tools {
        maven 'maven'
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
            nexusArtifactUploader artifacts: [
                [
                    artifactId: 'my-app', 
                    classifier: '', 
                    file: 'target/my-app-1.0.jar', 
                    type: 'jar'
                ]
            ], 
                credentialsId: 'nexuscredentials', 
                groupId: 'com.mycompany.app', 
                nexusUrl: '172.31.21.147:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'samplerepo', 
                version: '1.0'
            }
        }
    }
    }
