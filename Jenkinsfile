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
                script {

                    bat "curl \target\*.war \"http://localhost:8081/manager/text/deploy?path=/webapp&update=true\" --user admin:admin"
                }
                echo 'Deploy Stage Completed'
            }
        }
    }
}
