pipeline {
    agent any

    environment {
        // Absolute path to your company config folder
        FRONTEND_DIR = "${WORKSPACE}/frontend"
        COMPANY_CONFIGS = "C:/ProgramData/Jenkins/.jenkins/companyConfigs"
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

        stage('Setup Company Configs') {
            steps {
                // Log the folder path
                bat 'echo Company config folder path: %COMPANY_CONFIGS%'

                // List files in the config folder
                bat 'dir "%COMPANY_CONFIGS%"'

                // Optional: copy files into the workspace if needed
                bat 'xcopy /E /I /Y "%COMPANY_CONFIGS%" "%WORKSPACE%\\company-configs"'
            }
        }

        stage('Install Dependencies') {
            steps {
                dir("${FRONTEND_DIR}") {
                    sh 'npm install --legacy-peer-deps'
                }
            }
        }
    }
}
