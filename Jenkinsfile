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

    stage('Manual Approval') {
        input message: 'Apakah ingin dilanjutkan ke tahap deploy?', ok: 'Ya'
    }

    stage('Deploy') {
        docker.image(imageDocker).inside {
            sh './jenkins/scripts/deliver.sh'
            echo 'Aplikasi akan berjalan selama 1 menit sebelum otomatis diakhiri'
            sleep(time: 1, unit: 'MINUTES')
            echo 'Waktu telah habis, aplikasi akan diakhiri'
            sh './jenkins/scripts/kill.sh'
        }
    }
}
