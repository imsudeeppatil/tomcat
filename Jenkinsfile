pipeline {
    agent any

    tools {
        maven 'Maven 3.6.3'  // Use the Maven tool configured earlier
        jdk 'JDK 11'         // Use the JDK tool configured earlier
    }

    environment {
        TOMCAT_DIR = '/opt/tomcat/webapps'  // Tomcat directory path
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub
                git branch: 'main', url: 'https://github.com/username/MymavenWebApp01.git'
            }
        }

        stage('Build') {
            steps {
                // Run Maven clean install to build the project and generate the WAR file
                sh 'mvn clean install'
            }
        }

        stage('Deploy') {
            steps {
                // Copy the WAR file to Tomcat's webapps directory
                sh 'cp target/MymavenWebApp01-1.0-SNAPSHOT.war $TOMCAT_DIR/'
            }
        }

        stage('Start Tomcat') {
            steps {
                // Start Tomcat if not running
                sh '/opt/tomcat/bin/startup.sh'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
