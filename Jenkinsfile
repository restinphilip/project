pipeline {
    agent {
        label any
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

        stage('rds-setup') {
            steps {
               sh '''
                 mkdir test
                 unzip target/LoginWebApp.war
                 rm -rf LoginWebApp.war
                 rm -rf target/LoginWebApp.war
                 old= "jdbc:mysql://localhost:3300/test", "root","root"
                 new= "jdbc:mysql://database-1.cxgmm2giaw5y.ap-south-1.rds.amazonaws.com:3300/test" "admin","12345678"
                 sed -i 's/old/new userRegistration.jsp
                 zip LoginWebApp.war *
                 cp LoginWebApp.war target/
                '''
            }
        }  
        
        stage('deploy') {
            steps {
                sh '''
                    cp target/LoginWebApp.war /mnt/servers/apache-tomcat-10.1.48/webapps/
                '''
            }
        }
    }
}
