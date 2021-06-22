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
                copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: '${JOB_NAME}', selector: specific('${BUILD_NUMBER}'), target: '.'
                sh "sudo docker build . -t tomcatwebapp:${env.BUILD_NUMBER}"
            }
        }
    }
}