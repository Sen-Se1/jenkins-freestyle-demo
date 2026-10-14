
pipeline {
    agent any

    tools {
        maven 'Maven-3.10.0'
    }

    environment {
        IMAGE_NAME = 'devopsexample'
        IMAGE_TAG = "devopsexample:${BUILD_NUMBER}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sen-Se1/jenkins-freestyle-demo.git'
            }
        }

        stage('Build Project') {
            steps {
                withMaven(maven: 'Maven-3.10.0') {
                    bat 'mvn clean package'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                docker.build("${IMAGE_TAG}")
            }
        }

        stage('Deploy Container') {
            steps {
                docker.image("${IMAGE_TAG}").run(
                    '--name devopsexample -p 2222:2222'
                )
            }
        }
    }
}
