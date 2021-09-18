pipeline {
    agent any

    tools {
        maven 'maven3'
    }

    stages {

        stage ('Build') {
            steps{
                sh 'mvn clean package'
            }
        }

        stage ('Upload War to Nexus') {
            steps{
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: 'target/simple-app-1.0.0.war', 
                        type: 'war']
                    ], 
                        credentialsId: 'nexus3', 
                        groupId: 'in.javahome', 
                        nexusUrl: '10.0.0.6:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'http://20.101.8.47:8081/repository/simpleapp-release/', 
                        version: '1.0.0'

            }
        }

    }
}