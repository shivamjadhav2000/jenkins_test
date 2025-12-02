pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    credentialsId: 'jenkins_access',
                    url: 'git@bitbucket.org:ark-crm/crm.git'
            }
        }

        stage('Build') {
            steps {
                bat 'echo Running build ...'
            }
        }
    }
}
