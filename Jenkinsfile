pipeline {
    agent {label 'JAVA'}
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('git checkout') {
            steps {
                 git (
                    branch: 'main',
                    url: 'https://github.com/banothkranthinaik/spring-petclinic11.git'
                 )
            }
        }
        stage('build and scan') {
            steps {
                withCredentials([string(credentialsId: 'MYSONAR', variable: 'SONAR_TOKEN')]) {
                withSonarQubeEnv('SONAR') { 
                    sh """mvn package sonar:sonar \
                       -Dsonar.projectKey=banothkranthinaik_spring-petclinic11 \
                       -Dsonar.organization=banothkranthinaik \
                       -Dsonar.host.url=https://sonarcloud.io/ \
                       -Dsonar.login=$SONAR_TOKEN"""
                }
            }
        }
      }
    }
}