pipeline {
    agent any

    environment {
        IMAGE_NAME     = 'jenkins-freestyle-demo'
        CONTAINER_NAME = 'jenkins-freestyle-demo'
        HOST_PORT      = '8081'
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
                build job: 'maven-build-job',
                    wait: true,
                    propagate: true
            }
        }

        stage('Initialize Docker') {
            steps {
                withDockerServer([uri: 'unix:///var/run/docker.sock']) {
                    echo 'Docker server endpoint configured successfully.'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    withDockerServer([uri: 'unix:///var/run/docker.sock']) {
                        dockerImage = docker.build("${IMAGE_NAME}:${BUILD_NUMBER}")
                        dockerImage.tag('latest')
                    }
                }
            }
        }

        stage('Deploy Docker Image') {
            steps {
                script {
                    withDockerServer([uri: 'unix:///var/run/docker.sock']) {
                        sh "docker rm -f ${CONTAINER_NAME} || true"
                        docker.image("${IMAGE_NAME}:latest")
                              .run("--name ${CONTAINER_NAME} -p ${HOST_PORT}:8080")
                    }
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