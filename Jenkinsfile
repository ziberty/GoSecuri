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
//         stage('Test') {
//             steps {
//                 sh 'mvn test'
//             }
//             post {
//                 always {
//                     junit 'target/surefire-reports/*.xml'
//                 }
//             }
//         }
        stage('Execute') {
            steps {
                dir("target") {
                    sh 'java -jar goSecuri-1.0.jar'
                }
            }
        }
        stage('Send') {
            steps {
                sh 'scp -P 11749 -i ~/.ssh/id_rsa -r /var/jenkins_home/workspace/MSPR_APPLI/web gosecuri@8.tcp.ngrok.io:/var/www/gosecuri_web'
            }
        }
    }
}
