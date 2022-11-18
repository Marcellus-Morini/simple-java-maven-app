pipeline {
    agent any
    tools {
        maven 'maven-3.6.3'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Marcellus-Morini/simple-java-maven-app'
            }
        }
        stage('Build') {
            steps {
                sh script: 'mvn -B -DskipTests clean package'
            }
        }
        stage('Upload jar to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'my-app', 
                        classifier: '', 
                        file: 'target/my-app-1.0-SNAPSHOT.jar', 
                        type: 'jar'
                    ]
                ], 
                credentialsId: 'nexus', 
                groupId: 'com.mycompany.app', 
                nexusUrl: '172.31.15.167:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'simple-java-maven-app-release', 
                version: '1.0-SNAPSHOT'
            }
        }
    }
}
