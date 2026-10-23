
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Code downloaded from GitHub'
            }
        }

        stage('Test HTML') {
            steps {
                script {
                    if (isUnix()) {
                        sh "grep -q '<h1>' index.html"
                    } else {
                        bat 'findstr /C:"<h1>" index.html'
                    }
                }
                echo 'HTML test passed!'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'mkdir -p deploy && cp index.html deploy/index.html'
                    } else {
                        bat 'if not exist deploy mkdir deploy'
                        bat 'copy /Y index.html deploy\\index.html'
                    }
                }
                archiveArtifacts artifacts: 'deploy/index.html'
                echo 'Deployment successful!'
            }
        }
    }
}
