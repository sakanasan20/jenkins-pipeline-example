pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                build job: 'maven-project-package'
            }
            post {
                success {
                    echo 'Building... success'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploy to Staging...'
                build job: 'maven-project-deploy-to-staging'
            }
            post {
                success {
                    echo 'Deploy to Staging... success'
                }
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
