node {
    def customImage = docker.image('node:lts-buster-slim').using('-p 3000:3000')

    try {
        stage('Build') {
            checkout scm
            customImage.inside {
                sh 'npm install'
            }
        }

        stage('Test') {
            customImage.inside {
                sh './jenkins/scripts/test.sh'
            }
        }

        stage('Manual Approval') {
            input message: 'Lanjut ke tahap Deploy?'
        }

        stage('Deploy') {
            customImage.inside {
                sh './jenkins/scripts/deliver.sh'
                sleep(time: 1, unit: 'MINUTES')
                sh './jenkins/scripts/kill.sh'
            }
        }
    } finally {
        customImage.dismount()
    }
}
