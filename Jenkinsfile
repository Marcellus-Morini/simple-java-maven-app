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
    }
}
