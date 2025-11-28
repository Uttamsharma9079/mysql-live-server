pipeline {
    agent any

    environment {
        // Azure DevOps credentials stored in Jenkins (Username+PAT)
        AZURE_CREDS = credentials('azure-pat') // replace with your Jenkins credentials ID
        REPO_URL = 'https://dev.azure.com/azureclasses70989/project%20dev/_git/project%20dev'
        BRANCH = 'master'  // your branch
    }

    stages {
        stage('Checkout Repository') {
            steps {
                // Checkout code using PAT credentials
                git url: "${REPO_URL}", branch: "${BRANCH}", credentialsId: 'azure-pat'
            }
        }

        stage('Add/Commit SQL File') {
            steps {
                script {
                    // Ensure your .sql file is here. Adjust the path if needed
                    sh 'git add database.sql'
                    sh 'git commit -m "Add/update MySQL file" || echo "No changes to commit"'
                }
            }
        }

        stage('Push Changes') {
            steps {
                script {
                    // Push changes to Azure Repo
                    sh """
                    git config user.name "Jenkins"
                    git config user.email "jenkins@example.com"
                    git push origin ${BRANCH}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'MySQL file successfully pushed to Azure Repos!'
        }
        failure {
            echo 'Something went wrong. Check the Jenkins logs.'
        }
    }
}
