pipeline {
    agent any
    tools {
        maven "3.6.0"
        jdk "JDK"
    }
    stages {
        stage('Initialize'){
            steps{
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/maven"
            }
        }
        stage('Build') {
            steps {
                dir("/var/lib/jenkins/workspace/demopipelinetask/my-app") {
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        stage('Send') {
            steps {
             sh 'scp -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null /var/lib/jenkins/workspace/demopipelinetask/my-app/target/goSecuri-1.0.jar gosecuri@192.168.48.133:/var/www/'  
            }
        }
     }
    post {
       always {
          junit(
        allowEmptyResults: true,
        testResults: '*/test-reports/.xml'
      )
      }
   } 
}
