import hudson.model.*
import jenkins.model.Jenkins


def buildNumber = currentBuild.number
def jenkinsURL = currentBuild.absoluteUrl
def jobName = env.JOB_NAME

pipeline {
    try {
        agent { docker { image 'maven:3.3.3' } }
        stages {
            stage ('execute sh file') {
                steps {
                    sh "cd ../folder"
                    sh "./hello-world.sh"
                }
            }
            stage ('display environment vars') {
                steps {
                    sh 'echo "Bulid Number = ${buildNumber}"'
                    sh 'echo "Job Name = ${jobName}"'
                    sh 'echo "Build URL = ${jenkinsURL}"'
                }
            }
            stage ('using jenkins core api') {
                steps {
                    script {
                        def job = Jenkins.instance.getItemByFullName(jobName)
                        sh 'echo "print job: ${job.getFullName()}"'
                        sh 'echo "checking dataType by calling getClass(): ${job.getClass()}"'
                        sh 'echo "get all properties: ${job.getAllProperties()}"'
                    }   
                }
            }
            stage('build') {
                steps {
                    sh 'mvn --version'
                }   
            }   
        }
    } catch(caughtError) {
        echo "caught error"
        error = caughtError
        currentBuild.result = "Failure"
        echo "${error}"
    }
    finally {
        if(error) {
            throw err
        }
    }
    

    // post {
    //     success {
    //         mail to: 'johne.vang1@gmail.com',
    //         subject: "Successful jenkins build for Build Number: ${BUILD_NUMBER}",
    //         body: "yay"
    //     }
    //     failure {
    //         echo 'failed'
    //         mail to: 'johne.vang1@gmail.com',
    //         subject: "failed pipeline for Build Number: ${BUILD_NUMBER}",
    //         body: "${JOB_NAME} failed. Here's is the Jenkins URL: ${JENKINS_URL} for build number ${BUILD_NUMBER}. \n "
    //     }   
    // }
}


