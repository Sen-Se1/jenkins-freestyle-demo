node {
    def mvnHome = tool 'Maven-3.10.0'
    def dockerImage
    def dockerImageTag = "devopsexample:${env.BUILD_NUMBER}"

    stage('Clone Repo') {
        git branch: 'main',
            url: 'https://github.com/Sen-Se1/jenkins-freestyle-demo.git'
    }

    stage('Build Project') {
        sh "\"${mvnHome}/bin/mvn\" clean package"
    }

    stage('Initialize Docker') {
        // Docker CLI is already installed on the Ubuntu VM.
        sh 'docker --version'
    }

    stage('Build Docker Image') {
        sh "docker build -t ${dockerImageTag} ."
    }

    stage('Deploy Docker Image') {
        echo "Docker Image Tag Name: ${dockerImageTag}"

        sh """
            docker rm -f devopsexample || true
            docker run --name devopsexample \
                -d -p 2222:2222 ${dockerImageTag}
        """
    }
}
