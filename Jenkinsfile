pipeline {
    // Run on any available agent
    agent any

    // Trigger a build by polling SCM every 5 minutes.
    triggers {
        pollSCM('H/2 * * * *')
    }

    environment {
        // Define the Docker image name (adjust as necessary)
        DOCKER_IMAGE = "ecom-cicd"
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out the code from the GitHub repository
                // Adjust the branch if necessary (e.g., 'main' or 'master')
                git url: 'https://github.com/Mustafaml786/ecom-cicd.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Run your build command.
                // Here we assume a Maven project. For Windows, we use the 'bat' command.
                bat "mvn clean install"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Get the SonarQube Scanner tool (configured in Global Tool Configuration)
                    def scannerHome = tool 'SonarScanner'
                    
                    // Run the SonarQube analysis.
                    // withSonarQubeEnv uses the SonarQube server settings (name must match your Jenkins config)
                    withSonarQubeEnv('SonarQubeServer') {
                        // On Windows, run the sonar-scanner batch file.
                        bat "\"${scannerHome}\\bin\\sonar-scanner.bat\""
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build a Docker image using the Dockerfile in the repository root.
                bat "docker build -t ${DOCKER_IMAGE}:latest ."
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
