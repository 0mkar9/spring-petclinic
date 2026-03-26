pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Clone Code') {
            steps {
                git url: 'https://github.com/0mkar9/spring-petclinic.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t petclinic-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f petclinic-container || true
                docker run -d -p 8081:8080 --name petclinic-container petclinic-app
                '''
            }
        }
    }
}
