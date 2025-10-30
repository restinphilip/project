pipeline {
    agent any

    tools {
        maven 'apache-maven-3.9.11'
    }

    stages {
        stage('clean-repo') {
            steps {
                sh '''
                    echo "Cleaning old artifacts..."
                    rm -rf /root/.m2/repository/
                    rm -rf /mnt/servers/apache-tomcat-10.1.48/webapps/LoginWebApp*
                '''
            }
        }

        stage('clean-mvn-package') {
            steps {
                sh '''
                    echo "Building project with Maven..."
                    mvn clean package
                '''
            }
        }

        stage('cpy-remote-ec2') {
            steps {
                sh '''
                    echo "Copying WAR file to EC2..."
                    scp -i /root/mkey.pem target/LoginWebApp.war ec2-user@ec2-3-110-189-101.ap-south-1.compute.amazonaws.com:/mnt/servers/apache-tomcat-10.1.48/webapps/
                '''
            }
        }
    }
}
