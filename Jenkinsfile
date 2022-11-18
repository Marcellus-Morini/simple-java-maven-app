node {
    stage('Checkout') {
        git 'https://github.com/Marcellus-Morini/simple-java-maven-app'
    }
    stage('Build') {
        def mvnHome = tool name: 'maven-3.6.3', type: 'maven'

        sh "${mvnHome}/bin/mvn -B -DskipTests clean package"
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
