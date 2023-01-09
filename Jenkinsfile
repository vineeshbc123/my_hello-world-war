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
                sh 'docker login -u vineesh123 -p Vinusvini@2022'
                sh 'docker tag tomcat_build:${BUILD_NUMBER} vineesh123/mytomcat_new:${BUILD_NUMBER}'
                sh 'docker push vineesh123/mytomcat_new:${BUILD_NUMBER}'
            }
        } 
        stage( 'my deploy' ) {
        agent {label 'slave2'} 
            steps {
               sh 'docker pull vineesh123/mytomcat_new:${BUILD_NUMBER}'
               sh 'docker rm -f mytomcat'
               sh 'docker run -d -p 8080:8080 --name mytomcat vineesh123/mytomcat_new:${BUILD_NUMBER}'
            }
        }    
    } 
}
