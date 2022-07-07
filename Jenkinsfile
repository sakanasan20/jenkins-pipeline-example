pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn clean package --batch-mode'
            }
            post {
                success {
                    echo 'Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}
