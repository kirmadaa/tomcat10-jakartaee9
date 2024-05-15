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
                    // List the .war file in the target directory using Windows command
                    def warFile = bat(script: 'for %i in (target\\*.war) do @echo %i', returnStdout: true).trim()
                    
                    // The `warFile` will contain extra output, so we need to extract the actual file path
                    def warFilePath = warFile.split('\r\n').last().trim()
                    
                    // Deploy the built .war file to Tomcat
                    bat "curl --upload-file ${warFilePath} \"http://localhost:8081/manager/text/deploy?path=/webapp&update=true\" --user admin:admin"
                }
                echo 'Deploy Stage Completed'
            }
        }
    }
}
