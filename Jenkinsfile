pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('actividad3-php-fpm', '.')
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    docker.image('actividad3-php-fpm').withRun('-p 8097:80') {
                        sh 'curl http://localhost:8097/index.php'
                    }
                }
            }
        }
        
        stage('Deploy') {
            environment {
                DB_HOST = 'db'
                DB_NAME = 'postgres'
                DB_USER = 'postgres'
                DB_PASS = credentials('Jean1804')
            }
            steps {
                script {
                    docker.image('actividad3-php-fpm').push('my-registry/actividad3-php-fpm')
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}
