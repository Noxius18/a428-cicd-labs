node {
    def imageDocker = 'node:16-buster-slim'

    stage('Clone Repository') {
        checkout scm
    }

    stage('Build') {
        docker.image(imageDocker).inside {
            sh 'npm install'
        }
    }

    stage('Test') {
        docker.image(imageDocker).inside {
            sh './jenkins/scripts/test.sh'
        }
    }
}