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
        stage('Deploy to Production') {
            steps {
                timeout(time: 5, unit: 'DAYS') {
                    input message: 'Apprive production deployment?'
                }
                build job: 'maven-project-deploy-to-production'
            }
            post {
                success {
                    echo 'Deployed to Production... success'
                }
                failure {
                    echo 'Deployed to Production... failed'
                }
            }
        }
    }
}
