pipeline {
    agent {label 'slave1'} 
    stages {
        stage('My Build') { 
            steps {
              sh 'mvn package'
              sh 'pwd'
              sh 'whoami'
              sh 'scp -R /home/vineesh/workspace/declarative/target/hello-world-war-1.0.0.war ubuntu@172.31.7.201:/opt/apache-tomcat-10.0.27/webapps/'
            }
        }
        stage('My deploy') { 
        agent {label 'slave2'}
            steps {
              sh 'pwd'
              sh 'sudo sh /opt/apache-tomcat-10.0.27/bin/shutdown.sh'
              sh 'sleep 2'
              sh 'sudo sh /opt/apache-tomcat-10.0.27/bin/startup.sh'
            }
        }
    }
}
