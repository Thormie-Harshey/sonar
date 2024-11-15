pipeline {
    
	agent any
    tools {
	    maven "maven3"
	    jdk "java17"
	}
	
    stages{
        
        stage ('fetch code') {
            steps {
                git branch: 'java', url: 'https://github.com/seunayolu/sonarqube-jenkins.git'
            }
        }
        stage('build-app'){
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('build-app'){
            steps {
                sh 'mvn clean compile -DskipTests'
            }
        }

        stage('code analysis with sonarqube') {
          
		  environment {
             scannerHome = tool 'sonar-scanner-6'
          }
          steps {
            withSonarQubeEnv('sonar-server') {
               sh '''${scannerHome}/bin/sonar-scanner \
                   -Dsonar.projectKey=java-app \
                   -Dsonar.projectName=javaapp-repo \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/main/java \
                   -Dsonar.java.binaries=target/classes \
                   -Dsonar.organization=myreg-app'''
            }
          }
        }
    }
}
