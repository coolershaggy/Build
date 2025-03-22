pipeline {
    agent any

    triggers {
        // Poll SCM for changes every 5 minutes
        pollSCM('H/5 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull the source code from the Git repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Create the build directory and run CMake and Make using Windows batch commands
                bat '''
                if not exist build mkdir build
                cd build
                cmake .. 
                make
                '''
            }
        }

        stage('Test') {
            steps {
                // Run the compiled program from the build directory
                bat '''
                cd build
                project-build
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed!'
        }
        success {
            echo 'Build and Test stages succeeded!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs for details.'
        }
    }
}