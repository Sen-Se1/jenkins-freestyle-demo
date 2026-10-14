pipeline {
    agent any

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
                echo 'Repository cloned successfully!'
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

        stage('Initialize Docker') {
            steps {
                withDockerServer([
                    uri: 'unix:///var/run/docker.sock',
                    credentialsId: ''
                ]) {
                    echo 'Docker server initialized successfully!'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def appImage = docker.build(
                        "${IMAGE_NAME}:latest"
                    )
                    echo "Docker image built: ${IMAGE_NAME}:latest"
                }
            }
        }

        stage('Deploy Docker Container') {
            steps {
                script {
                    docker.image("${IMAGE_NAME}:latest").run(
                        "-d --name ${CONTAINER_NAME} -p ${HOST_PORT}:${CONTAINER_PORT}"
                    )
                    echo "Docker container ${CONTAINER_NAME} started successfully!"
                }
            }
        }
    }

    post {
        success {
            echo 'All pipeline stages completed.'
        }
        failure {
            echo 'Pipeline failed. Check the Console Output.'
        }
    }
}