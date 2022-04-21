pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Recuperation des sources') {
            steps {
               git branch: 'main', url: 'https://github.com/ziberty/GoSecuri.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Execute') {
            steps {
                dir("target") {
                    sh 'java -jar goSecuri-1.0.jar'
                    sh 'mv /web ../'
                }
            }
        }
        stage('Test') {
             steps {
                 sh 'ls -al'
                 sh 'mvn test'
             }
             post {
                 always {
                     junit 'target/surefire-reports/*.xml'
                   }
            }
        }
        stage('Send') {
            steps {
                sh 'scp -i ~/.ssh/id_rsa -r /var/jenkins_home/workspace/MSPR_APPLI/web gosecuri@192.168.220.134:/var/www/gosecuri_web'
            }
        }
    }
}
