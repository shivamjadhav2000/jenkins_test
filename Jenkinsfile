pipeline {
    agent any

    environment {
        CI = false
        FRONTEND_DIR = "${WORKSPACE}/frontend"
        COMPANY_CONFIGS_SRC = "C:/ProgramData/Jenkins/.jenkins/companyConfigs"
        COMPANY_CONFIGS_TARGET = "${WORKSPACE}/companyConfigs"
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
                bat 'echo Company config folder path: %COMPANY_CONFIGS_SRC%'
                bat 'dir "%COMPANY_CONFIGS_SRC%"'
                bat 'xcopy /E /I /Y "%COMPANY_CONFIGS_SRC%" "%COMPANY_CONFIGS_TARGET%"'
            }
        }

        stage('Install Dependencies') {
            steps {
                dir("${FRONTEND_DIR}") {
                    bat 'npm install --legacy-peer-deps'
                }
            }
        }

        stage('Build per Company') {
            steps {
                script {
                    def companies = ['company1'] // Or auto-detect later

                    companies.each { company ->
                        def envFile = "${COMPANY_CONFIGS_TARGET}\\${company}\\.env"
                        def staticDir = "${COMPANY_CONFIGS_TARGET}\\${company}\\static"
                        def buildOutputDir = "${FRONTEND_DIR}\\builds\\${company}"

                        dir("${FRONTEND_DIR}") {
                            bat """
                                echo Building for ${company}...

                                if exist "${envFile}" copy "${envFile}" ".env"

                                export CI=false
                                npm run build

                                if not exist "${buildOutputDir}" mkdir "${buildOutputDir}"
                                if exist "${buildOutputDir}" rd /s /q "${buildOutputDir}" && mkdir "${buildOutputDir}"

                                xcopy /E /I /Y "build\\*" "${buildOutputDir}\\"

                                if exist "${staticDir}" xcopy /E /I /Y "${staticDir}\\*" "${buildOutputDir}\\"

                                if exist ".env" del ".env"
                                if exist "build" rd /s /q "build"
                            """
                        }
                    }
                }
            }
        }
    }
}
