pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your repository
                git url: 'https://github.com/Mustafaml786/ecom-cicd.git'
            }
        }
        
        // Optional: Remove or disable the build stage if you don't need to build the project.
        // stage('Build') {
        //     steps {
        //         echo 'Skipping build stage since only SonarQube analysis is required.'
        //     }
        // }

        stage('SonarQube Analysis') {
            steps {
                // Set up the SonarQube environment (make sure 'SonarQube' matches the name you configured)
                withSonarQubeEnv('SonarQube') {
                    // If you configured the SonarQube Scanner as a tool in Jenkins, you can locate it by name.
                    def scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    
                    // Run the SonarQube scanner.
                    // If you have a sonar-project.properties file, this command is sufficient.
                    bat "\"${scannerHome}\\bin\\sonar-scanner\""
                    
                    // Alternatively, you can pass properties directly:
                    // bat "\"${scannerHome}\\bin\\sonar-scanner\" -Dsonar.projectKey=your_project_key -Dsonar.sources=."
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
