pipeline {
    agent none
    stages {
        stage('Test on Master') {
            agent { 
                label 'master'
            }
            steps {
                sh 'touch ${WORKSPACE}/master'
            }
        }
        stage('Test on Slave 1') {
            agent { 
                label 'slave-aws-1'
            }
            steps {
                sh 'touch ${WORKSPACE}/slave'
            }
        }
    }
}