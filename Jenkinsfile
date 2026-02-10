pipeline {
    agent any

    tools {
        maven 'Maven' // имя из UI Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/vahangevorgyan777/selenium-docker.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('Archive Results') {
            steps {
                archiveArtifacts artifacts: '**/target/surefire-reports/*.xml'
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }
}
