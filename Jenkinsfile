pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'mvn clean package --batch-mode'
            }
            post {
                success {
                    echo 'Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploy to Staging...'
                build job: 'maven-project-deploy-to-staging'
            }
        }
    }
}
