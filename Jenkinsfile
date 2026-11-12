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

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }

        stage('Copy Artifact for Deployment') {
    steps {
        bat '''
            if not exist "C:\\DeployedArtifacts\\staging" mkdir "C:\\DeployedArtifacts\\staging"
            dir target
            copy /Y "target\\student-app-1.0.jar" "C:\\DeployedArtifacts\\staging\\student-app-1.0.jar"
        '''
    		}
   	}

        stage('Deploy using Ansible') {
            steps {
                bat 'schtasks /run /tn "\\AnsibleDeploy"'
            }
        }
    }
}