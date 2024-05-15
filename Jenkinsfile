pipeline {
    agent any
    tools {
        maven 'Maven'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Starting Build Stage'
                withMaven(maven: 'Maven') {
                    // Build the project with Maven
                    bat 'mvn --version' // Verify Maven version for debugging
                    bat 'mvn clean package'
                }
                echo 'Build Stage Completed'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Starting Deploy Stage'
                bat 'copy /y .\\target\\*.war "C:\\Program Files\\Apache Software Foundation\\Tomcat 10.1\\webapps"'
                echo 'Deploy Stage Completed'
            }
        }
    }
}
