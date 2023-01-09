pipeline {
    agent {label 'slave1'}
    stages {
        stage('my Build') {
            steps {
                sh "echo ${BUILD_VERSION}"
                sh 'docker build -t tomcat_build:${BUILD_VERSION} .'
            }
        }  
        stage('publish stage') {
            steps {
                sh "echo ${BUILD_VERSION}"
                sh 'docker login -u vineesh123 -p Vinusvini@2022'
                sh 'docker tag tomcat_build:${BUILD_VERSION} vineesh123/mytomcat_new:${BUILD_VERSION}'
                sh 'docker push vineesh123/mytomcat_new:${BUILD_VERSION}'
            }
        } 
        stage( 'my deploy' ) {
        agent {label 'slave2'} 
            steps {
               sh 'docker pull vineesh123/mytomcat_new:${BUILD_VERSION}'
               sh 'docker rm -f mytomcat_new'
               sh 'docker run -d -p 8088:8080 --name mytomcat vineesh123/mytomcat_new:${BUILD_VERSION}'
            }
        }    
    } 
}
