def mvnHome

pipeline {
    agent {
        label 'ubuntu'
    }
    parameters {
        mvnHome = tool name: 'maven-3.6.3', type: 'maven'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Marcellus-Morini/simple-java-maven-app'
            }
        }
        stage('Build') {
            steps {
                sh "${mvnHome}/bin/mvn -B -DskipTests clean package"
            }
        }
        stage('Test') {
            steps {
                sh "${mvnHome}/bin/mvn test"
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }
}
