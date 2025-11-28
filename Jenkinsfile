pipeline {
    agent any

    environment {
    GITHUB_CREDS = credentials('my-github-creds') // replace with your actual credential ID
}

stages {
    stage('Checkout Repository') {
        steps {
            git url: "${REPO_URL}", branch: "${BRANCH}", credentialsId: 'my-github-creds'
        }
    }
}

    stages {
        stage('Checkout Repository') {
            steps {
                git url: "${REPO_URL}", branch: "${BRANCH}", credentialsId: 'github-credentials-id'
            }
        }

        stage('Add/Commit SQL File') {
            steps {
                script {
                    // On Windows, use bat instead of sh
                    bat 'git add database.sql'
                    bat 'git commit -m "Add/update MySQL file" || echo No changes to commit'
                }
            }
        }

        stage('Push Changes') {
            steps {
                script {
                    bat 'git config user.name "Jenkins"'
                    bat 'git config user.email "jenkins@example.com"'
                    bat 'git push origin ${BRANCH}'
                }
            }
        }
    }

    post {
        success {
            echo 'MySQL file successfully pushed to GitHub!'
        }
        failure {
            echo 'Something went wrong. Check the Jenkins logs.'
        }
    }
}
