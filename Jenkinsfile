pipeline {
    agent any
    tools {
        maven 'localMaven' 
    }
    stages{
        stage('Build'){
            agent {label 'master'}
            steps {
                sh 'mvn clean package'
                sh "docker build . -t tomcatwebapp:${env.BUILD_NUMBER}"
            }
        }
    }
}