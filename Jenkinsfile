pipeline {

    agent { docker { image 'maven:3.3.3' } }
    stages {
        stage ('display environment vars') {
            echo "Bulid Number = ${env.BULID_NUMBER}"
            echo "Job Name = ${env.JOB_NAME}"
            echo "Build URL = ${JENKINS_URL}"
        }
        stage('build') {
            steps {
                sh 'mvn --version'
            }   
	    }   
    }
    post {
        failure {
            echo 'failed'
            mail to: 'johne.vang1@gmail.com',
            subject: "failed pipeline for Build Number: ${BUILD_NUMBER}",
            body: "${JOB_NAME} failed. Here's is the Jenkins URL: ${JENKINS_URL} for build number ${BUILD_NUMBER}. \n "
        }   
    }
}


