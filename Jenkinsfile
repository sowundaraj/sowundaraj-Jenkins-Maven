pipeline {
    agent any
    tools { 
        maven 'mymaven' 
    }
    environment {
    imageName = 'ragh19/mavenjenkins'
    registrycred = 'DockerHub'
    dockerImage = ''
        
    }
    

    stages {
        stage('Pulling the Code From Github') {
            steps {
                git branch: 'main', url: 'https://github.com/raghavag1997/Docker-Jenkins-Maven.git'
            }
        }
        stage('Bulding the code') {
            steps {
                sh 'mvn compile'
                sh 'mvn package'
                sh 'mvn install'
            }
        }
        stage('Bulding the Image') {
            steps {
                script {
                  dockerImage  = docker.build imageName + ":$BUILD_NUMBER"
                }
            }
        }
        
        stage('Publishing the Image') {
            steps {
                script {
                    docker.withRegistry( '', registrycred ) {
                    dockerImage.push()
                    }
                }
            }
        }
    }
}

