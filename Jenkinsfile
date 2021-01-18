pipeline {

    agent {
        node {
            label 'master'
        }
    }

    environment {
        RUN_AUTOMATIONTEST = 'yes'
        IS_AUTOMATION_TEST = 'yes'
    }
    stages {

       // stage('Cleanup Workspace') {
       //     steps {
       //         script {
       //             try {
       //                 echo "start timeout"
       //                 timeout(time: 3,unit: 'SECONDS') {
       //                     build job: 'simple-pipline-test/develop', parameters: [ string(name: 'ENVIRONMENT_TAG', value: 'cap'),string(name: 'FORCE_RUN', value: 'yes')]
       //                 }
       //             } catch (Exception e) {
       //                 echo "downstream job run false"
       //             }
       //             currentBuild.result = 'ABORTED'
       //         }
       //     }
       // }

        stage(' Unit Testing') {
            when {
                anyOf {
                   branch 'PR-*'
                   allOf {
                       environment name: 'RUN_AUTOMATIONTEST', value: 'yes'
                       environment name: 'IS_AUTOMATION_TEST', value: 'yes'
                   }
                }
            }
            steps {
                sh """
                sleep 3
                echo "Running Unit Tests"
                """
                GitCommitID = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()
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
