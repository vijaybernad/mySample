pipeline {
    agent any
    tools {
        maven 'maven3' 
    }
   
    stages {
         stage('Create directory') {
            steps {
                sh "mkdir ${env.JOB_NAME}-${env.BUILD_NUMBER}"
            }
        }
        stage('Git clone/pull') {
            steps {
                echo 'Hello World'
                sh "cd ${env.JOB_NAME}-${env.BUILD_NUMBER}"
                sh "pwd"
                sh "mkdir testfolder"
                //git credentialsId: '3e5f4e40-ea03-40e3-9f96-2ac0956cb15f', url: 'https://github.com/vijaybernad/mySample'
            }
        }
       
        
        
    }
}
