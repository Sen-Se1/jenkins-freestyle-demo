
pipeline {
    agent any

    stages {
        stage('Test Docker Plugin') {
            steps {
                withDockerServer(
                    [uri: 'unix:///var/run/docker.sock', credentialsId: '']
                ) {
                    echo 'Docker Pipeline plugin step is working!'
                }
            }
        }
    }
}
