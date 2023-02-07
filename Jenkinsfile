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
					sshPublisher(publishers: [sshPublisherDesc(configName: 'QA-Server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: 'target/', sourceFiles: 'target/mvn-hello-world.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
			}
        }
    }
}
