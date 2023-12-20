pipeline {
     tools{
        maven 'mymaven'
    }
    agent {
        label 'JenkinAgent1'
    }
    stages {
        stage('Git Checkout') {
            steps {
                git url: 'https://github.com/Radhika622/calcwebapp-sonar.git'    
		            echo "Code Checked-out Successfully!!";
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compile'    
		            echo "Maven compile Goal Executed Successfully!";
            }
        }
	    
        stage('Clean and  Install') {
            steps {
                sh 'mvn clean install'    
		            echo "Maven Package Goal Executed Successfully!";
            }
        }
        
        stage('JUnit Reports') {
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
