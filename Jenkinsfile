pipeline {
    agent any
    
    environment {
        MAVEN_HOME = tool 'Maven'
    }

    stages {
        stage('Build') {
            steps {
                bat "\"${MAVEN_HOME}\\bin\\mvn\" clean package"
            }
        }

        stage('Stop Service') {
            steps {
             	     bat "net stop ConfigServer"
             	     sleep time: 10, unit: 'SECONDS'
             	     bat 'sc query ConfigServer | find "STATE" | find "STOPPED" && echo "Service stopped"'  
            }
        }

 		stage('Copy Jar File') {
            steps {
                bat "copy /Y target\\ConfigServer.jar G:\\HRMS_API\\ConfigServer"
            }
        }
    }
    post {
        always {
           bat "nssm start ConfigServer"
        }
    }
}