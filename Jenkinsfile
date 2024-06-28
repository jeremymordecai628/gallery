pipeline {
    agent any

    triggers {
        // Trigger a build whenever there's a push to the repository
        githubPush()
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy to Render') {
            steps {
                sh 'node server'
            }
        }
    }
}