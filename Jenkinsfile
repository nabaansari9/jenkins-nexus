pipeline {
    agent any
    tools {
        maven "Maven"
    }
    stages {
        stage("Clone code from GitHub") {
            steps {
                script {
                    git branch: 'main', credentialsId: 'GitHub_Cred', url: 'https://github.com/nabaansari9/jenkins-nexus.git';
                }
            }
        }
        stage("Maven Build") {
            steps {
                script {
                    sh "mvn package -DskipTests=true"
                }
            }
        }
        stage("Publish to Nexus Repository Manager") {
            steps {
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'my-app', 
                        classifier: '', 
                        file: 'target/Hello World-1.0-SNAPSHOT.war', 
                        type: 'war'
                        ]
                    ], 
                    credentialsId: 'NEXUS_CRED', 
                    groupId: 'com.mycompany.app', 
                    nexusUrl: 'http://54.226.101.58:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'maven-central-repository', 
                    version: '1.0-SNAPSHOT'

            }
        }
    }
}
