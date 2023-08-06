pipeline {
    agent {
        node {
            label 'maven'
        }
    }

environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
}
    stages {
        stage('build') {
            steps {
                echo "----------------Build Started------------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "----------------Build Completed------------"
            }
        }
        stage("test"){
            steps{
                echo "----------------Unit test Started------------"
                sh 'mvn surefire-report:report'
                echo "----------------Unit test end------------"
            }
        }

        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'triplebytes-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('triplebytes-sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
                sh "${scannerHome}/bin/sonar-scanner"
                }
            }

           
     }

    }
}
