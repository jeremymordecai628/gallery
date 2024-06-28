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

    post {
        success {
            slackSend(channel: '#Modex.IT-devops', message: "Build #${env.BUILD_ID} deployed successfully. Check it out at ${env.BUILD_URL}")
        }
        failure {
            slackSend(channel: '#Modex.IT-devops', message: "Build #${env.BUILD_ID} failed. Check details at ${env.BUILD_URL}")
            mail to: 'jeremy.mordecai@student.moringaschool.com',
                 subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                 body: "Something went wrong. Please check the Jenkins console output for more details."
        }
    }
}
