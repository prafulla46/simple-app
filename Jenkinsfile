pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                
                  nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', file: 'target/simple-app-3.0.0-SNAPSHOT', type: 'war']], credentialsId: '', groupId: 'in.javahome', nexusUrl: '172.31.70.123', nexusVersion: 'nexus3', protocol: 'http', repository: 'simpleapp-release', version: '3.0.0-SNAPSHOT'
                    }
            }
        }
}

