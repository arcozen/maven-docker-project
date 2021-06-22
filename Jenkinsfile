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
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('BuildImage'){
            agent {label 'aws-client'}
            steps {
                sh "pwd"
                echo "prima di copiare artifacts dal master"
                sh "sudo docker build . -t tomcatwebapp:${env.BUILD_NUMBER}"
            }
        }
    }
}