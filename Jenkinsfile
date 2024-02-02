pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage("Creación del archivo") {
            steps {
                echo "Creando el archivo"
                writeFile file: "archivo.txt", text: "prueba"
                echo "Archivo creado"
            }
        }

        stage("Subiendo el archivo a S3") {
            steps {
                script {
                    withAWS(credentials: 'AWS', region: 'us-east-1') {
                        s3Upload(file: 'archivo.txt', bucket: 'sprint7lab3', path: 'archivo.txt')
                    }
                }
            }
        }

        stage("Descargando el archivo de S3") {
            steps {
                script {
                    withAWS(credentials: 'AWS', region: 'us-east-1') {
                        s3Download(file: 'archivo.txt', bucket: 'sprint7lab3', path: 'archivo.txt', force: true)
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Fin del pipeline"
        }
    }
}
