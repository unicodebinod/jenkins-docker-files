pipeline {
    agent any
    environment {
    VERSION = '1.0'
    }
    stages {
        stage('Build') {
            steps {
                sh "/opt/apache-maven-3.8.6/bin/mvn package"
            }
        }
        stage('Test') {
            steps {
                sh "/opt/apache-maven-3.8.6/bin/mvn test"
            }
        }            
        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '''
                    docker build -t marcustechstarter/jenkinshub:${VERSION} .
                    docker login -u $USERNAME -p $PASSWORD
                    docker push marcustechstarter/jenkinshub:${VERSION} 
                    '''
                }
            }   
        }
    } 
}
