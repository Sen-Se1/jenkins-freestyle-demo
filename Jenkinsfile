
pipeline {
    agent any

    stages {
        stage('Test Git Plugin') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sen-Se1/jenkins-freestyle-demo.git'

                echo 'Git plugin executed successfully!'

                echo "Workspace: ${WORKSPACE}"

                echo "Build number: ${BUILD_NUMBER}"
            }
        }
    }
}
