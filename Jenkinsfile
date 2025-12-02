pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    tools {
        nodejs "nodejs"   // Name from Global Tool Config
    }

    environment {
        CI = false
        FRONTEND_DIR = "${WORKSPACE}\\frontend"
        BUILD_AUTOMATION_DIR = "${WORKSPACE}\\buildAutomation"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
                bat 'echo %FRONTEND_DIR% %BUILD_AUTOMATION_DIR%'
                bat 'dir %BUILD_AUTOMATION_DIR%'
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
                bat 'echo Building frontend...'
            }
        }
    }
}
