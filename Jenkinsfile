
pipeline {
    agent any

    stages {
        stage('Test Docker Plugin') {
            steps {
                withDockerServer('unix:///var/run/docker.sock') {
                    withDockerRegistry(credentialsId: '', url: '') {
                        echo 'Docker Pipeline plugin is available!'
                    }
                }
            }
        }
    }
}
