pipeline {
    agent {
        docker { image 'maven:3.9.2-openjdk-17' } // Maven + Java 17
    }

    environment {
        MAVEN_OPTS = "-Dmaven.repo.local=.m2/repository"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/vahangevorgyan777/selenium-docker.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive Results') {
            steps {
                archiveArtifacts artifacts: '**/target/surefire-reports/*.xml', allowEmptyArchive: true
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
        success {
            echo 'All tests passed ✅'
        }
        failure {
            echo 'Some tests failed ❌'
        }
    }
}
