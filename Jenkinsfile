pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-4.0.0-alpha-10/bin:$PATH"
}
    stages {
        stage("build"){
            steps {
                sh 'mvn clean deploy'
            }
        }
    stage ('SonarQube analysis'){
        environment {
            scannerHome = tool 'saurabh-sonar-scanner'
        }
        steps{
            withSonarQubeEnv('saurabh-sonarqube-server'){
                sh `${scannerHome}/bin/sonar-scanner`
            }
        }
    }
    }
}
