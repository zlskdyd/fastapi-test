pipeline {
    agent any

    environment {
        imagename = "zlskdyd/fastapi-test"
        registryCredential = 'zlskdyd'
        version = '1.0'
        dockerImage = ''
    }

    stages {

        // docker build
        stage('Bulid Docker') {
          agent any
          steps {
            echo 'Bulid Docker'
            script {
                dockerImage = docker.build("${imagename}:${version}", "--no-cache .")
            }
          }
          post {
            failure {
              error 'This pipeline stops here...'
            }
          }
        }

        // docker Deploy
        stage('Deploy Docker') {
          agent any
          steps {
            echo 'Deploy Docker '
            sh 'tag=${version} docker-compose -f ./docker/docker-compose.yml up -d'
          }
          post {
            failure {
              error 'This pipeline stops here...'
            }
          }
        }

    }
}
