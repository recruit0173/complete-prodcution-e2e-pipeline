pipeline {
    agent {
        label 'server1'
    }

    tools {
        jdk 'Java17'
        maven 'Maven3'
    }

    stages {
        stage('cleanup workspace') {
            steps {
                cleanWs()
            }
        }
        stage('checkout from SCM') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/recruit0173/complete-prodcution-e2e-pipeline.git'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add deploy commands here
            }
        }
    }
}