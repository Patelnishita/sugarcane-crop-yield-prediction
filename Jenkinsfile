pipeline {
    agent any

    environment {
        // This references the credential ID you created in Jenkins
        GITHUB_CREDS = credentials('github-creds')
        REPO_URL     = '://github.com'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Pulls the code from your GitHub repository
                git branch: 'main', 
                    credentialsId: 'github-creds', 
                    url: "https://${REPO_URL}"
            }
        }

        stage('Build & Test') {
            steps {
                echo 'Replace this section with your build commands (e.g., npm run build, mvn package, etc.)'
            }
        }

        stage('Upload to Git') {
            steps {
                // Authenticates and pushes updates or build logs back to your GitHub repository
                sh '''
                    git config user.name "Jenkins CI"
                    git config user.email "jenkins@yourdomain.com"
                    
                    # Example update: tracking the latest successful build time
                    echo "Last successful build: $(date)" > build_status.txt
                    
                    git add build_status.txt
                    
                    # Check if there are actual changes to commit to prevent pipeline errors
                    if ! git diff-index --quiet HEAD; then
                        git commit -m "Automated status update by Jenkins [skip ci]"
                        git push https://${GITHUB_CREDS_USR}:${GITHUB_CREDS_PSW}@${REPO_URL} HEAD:main
                    else
                        echo "No changes to upload."
                    fi
                '''
            }
        }
    }

    post {
        always {
            // Cleans up the workspace folder after the build finishes
            cleanWs()
        }
    }
}
