pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    tools {
        maven "apache-maven-3.8.1"
    }

    stages {
        stage('Clonar Repositorio') {
            steps {
                git 'https://github.com/KevinGuzmanY/contabilidad-back'
            }
        }

        stage('Construir') {
            steps {
                // Utilizar Maven para construir el proyecto
                sh 'apt install docker'
                sh 'docker-compose down'
                sh 'docker-compose build'
                sh 'docker-compose up -d'
            }
        }

        stage('Pruebas') {
            steps {
                // Ejecutar pruebas unitarias
                sh 'mvn test'
            }
        }

        stage('Empaquetar') {
            steps {
                // Empaquetar la aplicación en un archivo JAR/WAR
                sh 'mvn package'
            }
        }

        stage('Desplegar') {
            steps {
                // Desplegar la aplicación en el servidor de aplicación (por ejemplo, Tomcat)
                // Aquí debes incluir los comandos necesarios para el despliegue, por ejemplo:
                // sh 'scp target/nombre_de_tu_aplicacion.jar usuario@servidor:/ruta/donde/desplegar'
                echo 'El pipeline se ejecutó correctamente.'
            }
        }
    }

    post {
        success {
            // Acciones a realizar en caso de que el pipeline sea exitoso
            echo 'El pipeline se ejecutó correctamente.'
        }
        failure {
            // Acciones a realizar en caso de que el pipeline falle
            echo 'El pipeline falló. Por favor, revisa los registros para más detalles.'
        }
    }
}
