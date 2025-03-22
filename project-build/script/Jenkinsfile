pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *') // Polls for changes every 5 minutes
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull the source code
                checkout scm
            }
        }
        stage('Build') {
            steps {
                // Use CMake to configure and build the project
                sh 'mkdir -p build && cd build && cmake .. && make'
            }
        }
        stage('Test') {
            steps {
                // Run the compiled program
                sh './build/project-build'
            }
        }
    }
}