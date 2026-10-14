
pipeline {
    agent {
        label 'docker-agent'
    }

    environment {
        IMAGE_NAME     = 'jenkins-demo'
        CONTAINER_NAME = 'jenkins-demo'
        CONTAINER_PORT = '2222'
        HOST_PORT      = '2222'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sen-Se1/jenkins-freestyle-demo.git'
            }
        }

        stage('Build Project') {
            steps {
                withMaven(maven: 'Maven-3.10.0') {
                    sh 'mvn -B clean package'
                }
            }
            post {
                success {
                    archiveArtifacts(
                        artifacts: 'target/devOpsDemo-0.0.1-SNAPSHOT.jar',
                        fingerprint: true
                    )
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Deploy Docker Container') {
            steps {
                script {
                    docker.image("${IMAGE_NAME}:latest").run(
                        "-d --name ${CONTAINER_NAME} " +
                        "-p ${HOST_PORT}:${CONTAINER_PORT}"
                    )
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the Console Output.'
        }
    }
}
