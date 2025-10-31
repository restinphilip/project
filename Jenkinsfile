pipeline {
    agent {
           node {
        label 'qa'
                 }
          }
    tools {
        maven 'apache-maven-3.9.11'
          }

    stages {
        stage('clean-repo') {
            steps {
               sh '''
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

        stage('deploy') {
            steps {
                sh '''
                    cp target/LoginWebApp.war /mnt/servers/apache-tomcat-10.1.48/webapps/
                '''
            }
        }
    }
}
