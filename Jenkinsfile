pipeline {
    agent any
    stages {
        stage('git repo & clean') {
            steps {
                sh "rm /rf TicketBookingServiceJunitTesting"
                sh "git clone https://github.com/manju65char/TicketBookingServiceJunitTesting.git"
                sh "mvn clean -f TicketBookingServiceJunitTesting"
            }
        }
        stage('install') {
            steps {
                sh "mvn install -f firstpipelineproject"
            }
        }
        stage('test') {
            steps {
                sh "mvn test -f firstpipelineproject"
            }
        }
        stage('package') {
            steps {
                sh "mvn package -f firstpipelineproject"
            }
        stage('Deploy to QA AppServer') {
            steps {
				script {
                    sh 'scp target/TicketBookingServiceJunitTesting.war tomcat@aws-linux-machine:/usr/local/tomcat9/webapps/'			}
        }
    }
}
