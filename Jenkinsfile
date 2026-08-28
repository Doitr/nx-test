pipeline {
    agent {
        docker {
            image 'node:22-bookworm-slim'
        }
    }

    options {
        timestamps()
        timeout(time: 15, unit: 'MINUTES')
        disableConcurrentBuilds()
    }

    environment {
        CI = 'true'
    }

    stages {
        stage('Environment') {
            steps {
                sh 'node --version'
                sh 'npm --version'
            }
        }

        stage('Install') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Build') {
            steps {
                sh 'npx nx run-many -t build'
            }
        }
    }

    post {
        success {
            echo 'Nx build succeeded'
        }
        failure {
            echo 'Nx build failed'
        }
        always {
            deleteDir()
        }
    }
}