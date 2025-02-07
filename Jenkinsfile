pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your repository
                git url: 'https://github.com/Mustafaml786/ecom-cicd.git'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                // Set up the SonarQube environment (ensure 'SonarQube' matches your configured SonarQube server name in Jenkins)
                withSonarQubeEnv('SonarQube') {
                    // Wrap the Groovy code in a script block
                    script {
                        // Locate the SonarQube Scanner tool installed/configured in Jenkins Global Tool Configuration.
                        def scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                        
                        // Execute the SonarQube scanner using the batch command (use 'sh' instead of 'bat' if on Linux)
                        bat "\"${scannerHome}\\bin\\sonar-scanner\""
                    }
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
