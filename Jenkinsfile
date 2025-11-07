pipeline {
    agent {
        label 'build'
          }
    tools {
        maven 'apache-maven-3.9.11'
          }

    stages {
        stage('clean-repo') {
            steps {
               sh '''
                  sudo rm -rf /root/.m2/repository/*
                  sudo rm -rf /mnt/servers/apache-tomcat-10.1.48/webapps/LoginWebApp*
                '''
            }
        }

        stage('clean-mvn-package') {
            steps {
                sh '''
                   mvn clean package
                '''
            }
        }

        stage('deploy') {
            steps {
                sh '''
                    scp -i /mkey.pem target/LoginWebApp.war ec2-user@:  /mnt/servers/apache-tomcat-10.1.48/webapps/
                '''
            }
        }
    }
}
