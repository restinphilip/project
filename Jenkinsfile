pipeline {
    agent {
        node {
            label 'built-in'      
            customWorkspace '/mnt/scp-mvn'
        }
    }
    tools {
        maven 'apache-maven-3.9.11'
    }

    stages {
        stage('clean-repo') {
            steps {
                sh '''
                    rm -rf /root/.m2/repository/
                    rm -rf /mnt/servers/apache-tomcat-10.1.48/webapps/LoginWebApp*
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

        stage('cpy-remote-ec2') {
            steps {
                sh '''
                    scp -i /root/mkey.pem target/LoginWebApp.war ec2-user@ec2-3-110-189-101.ap-south-1.compute.amazonaws.com:/mnt/servers/apache-tomcat-10.1.48/webapps/
                '''
            }
        }
    }
}
