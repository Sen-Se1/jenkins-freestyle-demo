
pipeline {
    agent any

    stages {
        stage('Test Docker Cloud') {
            steps {
                withDockerServer(
                    [
                        uri: 'unix:///var/run/docker.sock',
                        credentialsId: ''
                    ]
                ) {
                    echo 'Docker server configured successfully!'
                }
            }
        }
    }
}
