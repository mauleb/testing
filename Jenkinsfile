#!/usr/bin/env groovy

def hash

pipeline {
    agent linux

    stages {
        stage('Configure') {
            hash = sh(script: 'echo $(git log --pretty=format:\'%h\' -n 1)', returnStdout: true).trim()
        }

        stage('Build') {
            steps {
                script {
                    sh """
                        img build -t test:${hash} .
                    """
                }
            }
        }
    }
}