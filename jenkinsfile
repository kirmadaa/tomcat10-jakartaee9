pipeline {
    agent any

    tools {
        maven 'Maven 3.6.3'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the provided Git repository
                git 'git@github.com:kirmadaa/tomcat10-jakartaee9.git'
            }
        }
        
        stage('Build') {
            steps {
                // Build the project with Maven
                bat 'mvn clean package'
            }
        }
        
        stage('Deploy') {
            steps {
                // Deploy the built .war file to Tomcat
                bat 'curl --upload-file ./target/*.war "http://localhost:8081/manager/text/deploy?path=/webapp&update=true" --user admin:admin'
            }
        }
    }
}
