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
                def mavenPom = readMavenPom 'pom.xml'

                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: "target/simple-app-${mavenPom.version}.war", 
                        type: 'war']
                    ], 
                        credentialsId: 'nexus3', 
                        groupId: 'in.javahome', 
                        nexusUrl: '10.0.0.6:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'simpleapp-release', 
                        version: "${mavenPom.version}"

            }
        }

    }
}