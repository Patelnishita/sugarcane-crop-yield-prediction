pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Patelnishita/sugarcane-crop-yield-prediction'
            }
        }

        stage('Verify Files') {
            steps {
                sh 'pwd'
                sh 'ls -la'
            }
        }

        stage('Build') {
            steps {
                echo 'No build required for HTML project.'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
