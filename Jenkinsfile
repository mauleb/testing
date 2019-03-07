#!/usr/bin/env groovy

def hash

pipeline {
    agent {
        node {
            label 'linux'
        }
    }

    stages {
        stage('Configure') {
            steps {
                script {
                    hash = sh(script: 'echo $(git log --pretty=format:\'%h\' -n 1)', returnStdout: true).trim()
                    sh """
                        ls -al /var/run/docker.sock
                    """
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh """
                        docker build -t test:${hash} .
                    """
                }
            }
        }
    }
}