pipeline {
    agent any
    stages {
        stage('git checkout') {
            steps {
                git(credentialsId: 'git_credentials', url: 'https://github.com/Gabin-Crn/compile_app.git', branch: 'main')
            }
        }
        stage('Build the Maven application') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Unit Test Execution') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'docker build -t gabin1704/alpinegms .'
            }
        }
        stage('Image on DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhubpass', usernameVariable: 'dockerUsername', passwordVariable: 'dockerPassword')]) {
                    sh 'docker login -u $dockerUsername -p $dockerPassword'
                    sh 'docker push gabin1704/alpine'
                }
            }
        }
   
    }
}

