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
        stage('SonarQube scan') {
            steps {
                withSonarQubeEnv('sq-server') {
                    sh 'mvn clean sonar:sonar -Dsonar.projectKey=com.mycompany.app:my-app -Dsonar.host.url=http://3.8.180.251:9000 -Dsonar.login=759e346c268e1e3113fa3dc42a1763f854c69885'
                }
            }            
        }
        stage('SonarQube quality gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }            
        }        
        stage('Build') {
            steps {
                sh script: 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
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
