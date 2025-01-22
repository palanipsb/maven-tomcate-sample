 pipeline {     
    agent {label 'slave-1'} 
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    } 

    stages {        
        stage('Compile') {
            steps {
            sh  "mvn compile"
            }
        }
        stage('Tests') {
            steps {
                sh "mvn test"
            }
        }        
        stage('Build Package') {
            steps {
                sh "mvn cleanpackage"
            }
        }
        stage('Deploy Package') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcatserver-credential', path: '', url: 'http://4.206.37.40:8082/')], contextPath: 'Planview', onFailure: false, war: 'target/*.war'
            }
        }
    }
}
