pipeline {
    agent any

    tools {
        maven 'maven3'
    }

    options {
        buildDiscarder logRotator( daysToKeepStr: '5', numToKeepStr: '7')
    }
    
    stages {

        stage ('Build') {
            steps{
                sh 'mvn clean package'
            }
        }

        stage ('Upload War to Nexus') {
            steps{

                script {
                    def mavenPom = readMavenPom file : 'pom.xml'
                    def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "simpleapp-snapshot": "simpleapp-release"

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
                        repository: nexusRepoName, 
                        version: "${mavenPom.version}"
                }

            }
        }

    }
}