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
    }
    }
