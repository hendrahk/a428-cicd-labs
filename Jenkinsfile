node {
    docker.image('node:16').withRun('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }
    }
}
