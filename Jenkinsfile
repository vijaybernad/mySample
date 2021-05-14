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
        stage('Git clone/pull & Maven Build') {
            steps {
                echo 'Hello World'
                dir("${env.JOB_NAME}-${env.BUILD_NUMBER}") {
                    sh "mkdir testfolder"
                    git credentialsId: '3e5f4e40-ea03-40e3-9f96-2ac0956cb15f', url: 'https://github.com/vijaybernad/mySample'
                    sh 'mvn clean package'
                } 
            }
        }
        stage('Deploy application to tomcat') {
            steps {
                sshagent(['tomcatdev']) {
                     dir("${env.JOB_NAME}-${env.BUILD_NUMBER}") {
                    //rename the var file
                    sh 'mv target/*.war target/myweb.war'
                    sh "ssh ec2-user@172.31.37.57 mkdir -p /opt/tomcat8/webapps/${env.JOB_NAME}-${env.BUILD_NUMBER}"
                    //copy file to tomcat server
                    sh "scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@172.31.37.57:/opt/tomcat8/webapps/"
                    sh "ssh ec2-user@172.31.37.57 /opt/tomcat8/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.37.57 /opt/tomcat8/bin/startup.sh"
                }
              }
            }
        }
       
        
        
    }
}
