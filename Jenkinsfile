pipeline {
    agent any
    tools {
        maven 'M2_HOME'
    }
    stages {
        stage('SCM checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/classdevop/spring-boot-war-example.git']])
            }
        }
        stage('build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Deploy to test env') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-server', path: '', url: 'http://http://3.109.186.242/:8080/')], contextPath: '/app', war: '**/*.war'
            }
        }
    }
}


