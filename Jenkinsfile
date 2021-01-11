pipeline {

    agent {
        node {
            label 'master'
        }
    }

    stages {

        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                build job: 'simple-pipline-test/develop', parameters: [ string(name: 'ENVIRONMENT_TAG', value: 'cap')]
            }
        }

        stage(' Unit Testing') {
            steps {
                sh """
                echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                echo "Running Code Analysis"
                """
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                sh """
                echo "Building Artifact"
                """

                sh """
                echo "Deploying Code"
                """
            }
        }

    }
}
