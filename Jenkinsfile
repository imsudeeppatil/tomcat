pipeline {
    agent any

    tools {
        maven 'Maven'  // Reference to the Maven tool configured in Jenkins
        jdk 'JDK'      // Reference to the JDK tool configured in Jenkins
    }

    environment {
        TOMCAT_DIR = '/opt/tomcat/webapps'  // Path to Tomcat webapps directory
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository
                git branch: 'master', url: 'https://github.com/imsudeeppatil/tomcat.git'
            }
        }

        stage('Build') {
            steps {
                // Run Maven to clean and install the project, generate the WAR file
                sh 'mvn clean install'
            }
        }

        stage('Deploy') {
            steps {
                // Copy the generated WAR file to Tomcat's webapps directory
                sh 'cp target/MymavenWebApp01-1.0-SNAPSHOT.war $TOMCAT_DIR/'
            }
        }

        stage('Start Tomcat') {
            steps {
                // Start Tomcat (ensure Tomcat is not already running)
                sh '/opt/tomcat/bin/startup.sh'
            }
        }
    }

    post {
        success {
            // If the pipeline succeeds, echo success message
            echo 'Deployment successful!'
        }
        failure {
            // If the pipeline fails, echo failure message
            echo 'Deployment failed!'
        }
    }
}
