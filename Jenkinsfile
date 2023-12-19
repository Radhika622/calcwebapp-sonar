pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                git url: 'https://github.com/Radhika622/calcwebapp-sonar.git'    
		            echo "Code Checked-out Successfully!!";
            }
        }
        stage('Compile') {
            steps {
                bat 'mvn compile'    
		            echo "Maven compile Goal Executed Successfully!";
            }
        }
	    
        stage('Clean and  Install') {
            steps {
                bat 'mvn clean install'    
		            echo "Maven Package Goal Executed Successfully!";
            }
        }
        
        stage('JUNit Reports') {
            steps {
                    junit 'target/surefire-reports/*.xml'
		                echo "Publishing JUnit reports"
            }
        }
        
        stage('Jacoco Reports') {
            steps {
                  jacoco()
                  echo "Publishing Jacoco Code Coverage Reports";
            }
        }

	stage('SonarQube analysis') {
            steps {
		// Change this as per your Jenkins Configuration
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn package sonar:sonar'
                }
            }
        }

	stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
        
    }
    post {
        
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
    
    }
}
