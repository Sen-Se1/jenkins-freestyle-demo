
pipeline {
    agent any

    tools {
        maven 'Maven-3.10.0'
    }

    stages {
        stage('Test Maven Plugin') {
            steps {
                withMaven(maven: 'Maven-3.10.0') {
                    echo 'Maven plugin configured successfully!'
                }
            }
        }
    }
}
