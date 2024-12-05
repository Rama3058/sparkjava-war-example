pipeline {
    agent any

    // environment {
    //     MAVEN_HOME = tool name: 'Maven', type: 'maven'
    // }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository
                git branch: 'master', url: 'https://github.com/Rama3058/sparkjava-war-example.git'
            }
        }

        stage('Setup Maven') {
            steps {
                // Set up Maven environment
                echo "Using Maven from: ${MAVEN_HOME}"
                sh "${MAVEN_HOME}/bin/mvn -v"
            }
        }

        stage('Build Project') {
            steps {
                // Build the project and package the WAR file
                sh "${MAVEN_HOME}/bin/mvn clean package"
            }
        }

        stage('Archive WAR File') {
            steps {
                // Archive the generated WAR file
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }
    }

    post {
        always {
            // Clean workspace after build
            cleanWs()
        }
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Check logs for more details.'
        }
    }
}
