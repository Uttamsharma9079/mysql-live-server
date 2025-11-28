pipeline {
    agent any

    environment {
        // Replace 'my-github-creds' with your Jenkins GitHub credentials ID
        GITHUB_CREDS = credentials('my-github-creds')
        REPO_URL = 'https://github.com/Uttamsharma9079/mysql-live-server.git'
        BRANCH = 'main' // Change if your branch is 'master'
    }

    stages {
        stage('Checkout Repository') {
            steps {
                echo "Checking out repository..."
                git url: "${REPO_URL}", branch: "${BRANCH}", credentialsId: 'my-github-creds'
            }
        }

        stage('Add/Commit SQL File') {
            steps {
                script {
                    echo "Adding and committing database.sql..."
                    // Windows uses 'bat' instead of 'sh'
                    bat 'git add database.sql'
                    // Commit changes; if no changes, echo message instead of failing
                    bat 'git commit -m "Add/update MySQL file" || echo No changes to commit'
                }
            }
        }

        stage('Push Changes') {
            steps {
                script {
                    echo "Pushing changes to GitHub..."
                    // Configure Git user
                    bat 'git config user.name "Jenkins"'
                    bat 'git config user.email "jenkins@example.com"'
                    // Push to GitHub
                    bat 'git push origin ${BRANCH}'
                }
            }
        }
    }

    post {
        success {
            echo '✅ MySQL file successfully pushed to GitHub!'
        }
        failure {
            echo '❌ Something went wrong. Check the Jenkins logs.'
        }
    }
}
