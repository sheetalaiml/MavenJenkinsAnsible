pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Maven Project') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Check Ansible') {
            steps {
                bat 'wsl.exe -d Ubuntu -- ansible-playbook --version'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }
    }
}