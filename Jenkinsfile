@Library("shared-lib") _
pipeline {
    agent {
        label 'vinod'
    }

    stages {
        stage('Hello'){
            steps{
                script{
                    hello()
                }
            }
            
        }
        stage('Build & Start Containers') {
            steps {
                script{
                    clone("keshav bhai ka raj")
                }
            }
        }

        stage('Test Application') {
            steps {
                echo 'Testing application'

                sh '''
                sleep 20

                docker compose ps

                curl -f http://localhost:8000 || exit 1
                '''

                echo 'Application is healthy'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Application deployed successfully'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully'
        }

        failure {
            echo 'Pipeline failed'

            sh '''
            docker compose ps || true
            docker compose logs --tail=50 || true
            '''
        }
    }
}