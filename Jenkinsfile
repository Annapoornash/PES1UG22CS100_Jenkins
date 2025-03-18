pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          userRemoteConfigs: [[url: 'https://github.com/YourRepo/YourRepoName']]])
            }
        }

        stage('Build') {
            steps {
                script {
                    // Introduced intentional failure
                    echo "Building the project..."
                    sh 'g++ non_existent_file.cpp -o output'  // This will fail since the file doesn't exist
                }
            }
        }

        stage('Test') {
            steps {
                echo "Testing the project..."
                sh './output'  // This will not run because the build stage failed
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the project...'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed!'  // This will run when any stage fails
        }
    }
}
