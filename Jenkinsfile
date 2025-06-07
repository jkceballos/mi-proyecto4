pipeline {
    agent any

    environment {
        DOCKER_HOST = 'unix:///var/run/docker.sock'
    }

    stages {
        stage('Construir contenedores') {
            steps {
                sh 'docker-compose build --no-cache'
            }
        }

        stage('Verificar archivos en contenedor') {
            steps {
                sh 'docker-compose run --rm web ls -R /app'
            }
        }

        stage('Ejecutar pruebas') {
            steps {
                sh 'docker-compose run --rm web find . -name "test_app.py"'
                sh 'docker-compose run --rm web python tests/test_app.py'
            }
        }

        stage('Desplegar') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}