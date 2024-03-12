pipeline {
    agent any

    stages {
        stage('Off app') {
            steps {
                // Dừng các container đã được khởi chạy bằng lệnh docker-compose run
                sh 'docker-compose --project-name backend -f docker-compose.yml down'

                // Dừng các container đã được khởi chạy bằng lệnh docker-compose up
                sh 'docker-compose --project-name frontend -f docker-compose-frontend.yml down'
            }
}


        stage('Build and Deploy') {
            steps {
                sh 'docker compose run --rm backend setup'
                sh 'docker compose run --rm frontend npm install'
                sh 'docker compose up -d frontend'
            }
        }

        stage('Remove unused images') {
            steps {
                sh 'sudo docker image prune -a -f'
            }
        }

    }
}
