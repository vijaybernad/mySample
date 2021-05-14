pipeline {
    agent any
    tools {
        maven 'maven3' 
    }

    stages {
        stage('Git clone/pull') {
            steps {
                echo 'Hello World'
                git credentialsId: '3e5f4e40-ea03-40e3-9f96-2ac0956cb15f', url: 'https://github.com/vijaybernad/mySample'
            }
        }
        stage('Create directory') {
            steps {
                sh "mkdir ${env.JOB_NAME}"
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Deploy application to tomcat') {
            steps {
                sshagent(['tomcatdev']) {
                    //rename the var file
                    sh 'mv target/*.war target/myweb.war'
                    //copy file to tomcat server
                    sh 'scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@172.31.37.57:/opt/tomcat8/webapps'
                    sh "ssh ec2-user@172.31.37.57 /opt/tomcat8/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.37.57 /opt/tomcat8/bin/startup.sh"
                }
            }
        }
    }
}
