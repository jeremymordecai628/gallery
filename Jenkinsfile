pipeline {
    agent any

    triggers {
        // Trigger a build whenever there's a push to the repository
        githubPush()
    }

    stages {
        stage('Install Node.js and NPM') {
            steps {
                // Install the latest Node.js LTS and update NPM
                sh '''
                   curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
                   sudo apt-get install -y nodejs
                   npm install -g npm@latest
                '''
            }
        }
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
    post {
        success {
            slackSend (
                channel: '#yourfirstname_ip1',
                color: 'good',
                message: "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL}) succeeded."
            )
        }
        failure {
            slackSend (
                channel: '#yourfirstname_ip1',
                color: 'danger',
                message: "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL}) failed."
            )
        }
        always {
            slackSend (
                channel: '#yourfirstname_ip1',
                color: 'warning',
                message: "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL}) finished with status: ${currentBuild.currentResult}."
            )
        }
    }
}
