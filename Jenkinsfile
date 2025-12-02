pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Clone Repository') {
            steps {
                git branch: 'master',
                    credentialsId: 'jenkins_access',
                    url: 'https://bitbucket.org/ark-crm/crm.git'
            }
        }

        stage('Build') {
            steps {
                bat 'echo Running build ...'
            }
        }
    }
}
