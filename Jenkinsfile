pipeline {
    agent any

    stages {

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Run Backend Container') {
            steps {
                sh 'docker rm -f backend-container || true'
                sh 'docker run -d --name backend-container backend-app'
            }
        }

        stage('Run Nginx') {
            steps {
                sh 'docker rm -f nginx-container || true'
                sh '''
                docker run -d -p 8081:80 \
                --name nginx-container \
                -v $PWD/nginx/default.conf:/etc/nginx/conf.d/default.conf \
                nginx
                '''
            }
        }
    }
}
