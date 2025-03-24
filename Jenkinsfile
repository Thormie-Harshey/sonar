pipeline {
    
	agent any
    tools {
	    maven "maven3"
	    jdk "java17"
	}
	
    stages{
        
        stage ('fetch code') {
            steps {
                git branch: 'java', url: 'https://github.com/Thormie-Harshey/sonar.git'
            }
        }
        stage('build-app'){
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('app-compile'){
            steps {
                sh 'mvn clean compile -DskipTests'
            }
        }

        stage('code analysis with sonarqube') {
          
		  environment {
             scannerHome = tool 'sonar-scanner-7'
          }
          steps {
            withSonarQubeEnv('sonar-server') {
               sh '''${scannerHome}/bin/sonar-scanner \
                   -Dsonar.projectKey=humble-java-app \
                   -Dsonar.projectName=humble-java-app \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/main/java \
                   -Dsonar.java.binaries=target/classes \
                   -Dsonar.organization=humble-org'''
            }
          }
        }
    }
}
