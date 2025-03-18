pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout([$class: 'GitSCM',
                branches: [[name: '*/main']],
                userRemoteConfigs: [[url: 'https://github.com/Annapoornash/PES1UG22CS100_Jenkins']]])
            }
        }

        stage('Build') {
            steps {
                // Introduced error: This is an incorrect reference to a build.
                build 'PES1UG22CS100-1'  // This will fail because no such job exists.
                sh 'g++ main.cpp -o output'
            }
        }

        stage('Test') {
            steps {
                sh './output'
            }
        }

        stage('Deploy') {
            steps {
                echo 'deploy'
            }
        }
    }

    post {
        failure {
            error 'Pipeline failed'  // This will execute when any stage fails.
        }
    }
}
