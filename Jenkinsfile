pipeline {
    agent any
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/shivamjadhav2000/jenkins_test.git'
            }
        }

        stage('Build') {
            steps {
                bat 'echo Running build ...'
            }
        }
    }
}
