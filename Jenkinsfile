pipeline {
    agent {label 'slave1'}
    stages {
        stage('my Build') {
            steps {
                sh 'docker build -t tomcat_build:${BUILD_NUMBER} .'
            }
        }  
        stage('publish stage') {
            steps {
                sh "echo ${BUILD_NUMBER}"
                withCredentials([usernamePassword(credentialsId: 'Dockerhub', passwordVariable: 'DockerhubPassword', usernameVariable: 'DockerhubUser')]) {
                sh "docker login -u ${env.DockerhubUser} -p ${env.DockerhubPassword}"
                sh 'docker tag tomcat_build:${BUILD_VERSION} vineesh123/mytomcat_new:${BUILD_NUMBER}'
                sh 'docker push vineesh123/mytomcat_new:${BUILD_NUMBER}'
                }
            }
        } 
        stage( 'my deploy' ) {
        agent {label 'slave2'} 
            steps {
               sh 'docker pull vineesh123/mytomcat_new:${BUILD_NUMBER}'
               sh 'docker rm -f mytomcat'
               sh 'docker run -d -p 8088:8080 --name mytomcat vineesh123/mytomcat_new:${BUILD_NUMBER}'
            }
        }    
    } 
}
