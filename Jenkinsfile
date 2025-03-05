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

    stage('Deploy') {
        docker.image(imageDocker).inside {
            sh './jenkins/scripts/deliver.sh'
            timeout(time: 1, unit: 'MINUTES') {
                input message: 'Sudah selesai menggunakan React App? (klik "Proceed" untuk mengakhiri)'
            }
            sh './jenkins/scripts/kill.sh'
        }
    }
}