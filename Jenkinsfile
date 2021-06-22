pipeline {
    agent any
    tools {
        maven 'localMaven' 
    }
    stages{
        stage('BuildApp'){
            agent {label 'master'}
            steps {
                sh 'mvn clean package'
            }
        }
        stage('BuildImage'){
            agent {label 'awsClient'}
            steps {
                sh "docker build . -t tomcatwebapp:${env.BUILD_NUMBER}"
            }
        }
    }
}