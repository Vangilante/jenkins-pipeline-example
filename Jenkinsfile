import hudson.model.*
import jenkins.model.Jenkins


def buildNumber = currentBuild.number
def jenkinsURL = currentBuild.absoluteUrl
def jobName = env.JOB_NAME

pipeline {
    agent { docker { image 'maven:3.3.3' } }
    stages {
        stage ('display environment vars') {
            steps {
                echo "Bulid Number = ${buildNumber}"
                echo "Job Name = ${jobName}"
                echo "Build URL = ${jenkinsURL}"
            }
        }
        stage ('using jenkins core api') {
            steps {
                script {
                    def job = Hudson.instance.getJob(jobName)
                    echo "print job: ${job}"
                }   
            }
        }
        stage('build') {
            steps {
                sh 'mvn --version'
            }   
	    }   
    }
    post {
        success {
            mail to: 'johne.vang1@gmail.com',
            subject: "Successful jenkins build for Build Number: ${BUILD_NUMBER}",
            body: "yay"
        }
        failure {
            echo 'failed'
            mail to: 'johne.vang1@gmail.com',
            subject: "failed pipeline for Build Number: ${BUILD_NUMBER}",
            body: "${JOB_NAME} failed. Here's is the Jenkins URL: ${JENKINS_URL} for build number ${BUILD_NUMBER}. \n "
        }   
    }
}


