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