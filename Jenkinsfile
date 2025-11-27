pipeline {
    agent any

    tools {
        maven 'apache-maven-3.9.11'
    }

    stages {

        stage('clean-repo') {
            steps {
                sh '''
                    rm -rf ~/.m2/repository/*
                    rm -rf /mnt/servers/apache-tomcat-10.1.48/webapps/LoginWebApp*
                '''
            }
        }

        stage('clean-mvn-package') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('rds-setup') {
            steps {
                sh '''
            cd target
            unzip LoginWebApp.war
            sed -i 's|localhost|database-1.cxgmm2giaw5y.ap-south-1.rds.amazonaws.com|g' userRegistration.jsp
            sed -i 's|"root", "root"|"admin", "12345678"|g' userRegistration.jsp
            rm -f LoginWebApp.war
            zip -r LoginWebApp.war *
                '''
            }
        }

        stage('deploy') {
            steps {
                sh 'cp target/LoginWebApp.war ~/servers/apache-tomcat-10.1.49/webapps/'
            }
        }
    }
}
