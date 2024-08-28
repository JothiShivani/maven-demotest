pipeline {
    agent any
    
    environment {
     
        scannerHome = tool 'SonarQube Scanner'                   
        SONAR_TOKEN = 'ccb2f9a330bbe716189a142e162b3ea84cf44c2b'                            
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your version control system
                git 'https://github.com/JothiShivani/maven-demotest.git'
            }
        }
        
        stage('Build Maven Project') {
            steps {
                // Run the Maven build
                bat 'mvn clean install'
            }
        }

        stage('Run Unit Tests') {
            steps {
                // Run the unit tests
                bat 'mvn test'
            }
            post {
                always {
                    // Archive test results
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Run SonarCloud') {
            steps {
                withSonarQubeEnv('SonarQube Scanner') {
                
                //     -Dsonar.exclusion=**/*.java \
                //     -Dsonar.java.binaries=target/classes"
                


                bat "${scannerHome}/bin/sonar-scanner \
                -Dsonar.projectKey=JothiShivani_maven-demotest \
                -Dsonar.organization=jothishivani \
                -Dsonar.host.url=https://sonarcloud.io \         
                -Dsonar.login=${SONAR_TOKEN}" 
                

                }
            }
        }
        
        
        
    }
}
