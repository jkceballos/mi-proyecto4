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

        stage('Ejecutar pruebas') {
            steps {
                sh 'docker-compose run --rm web python -m unittest discover -s tests'
            }
        }

        stage('Desplegar') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}