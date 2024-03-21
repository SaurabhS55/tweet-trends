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
                 echo "----------- build started ----------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                 echo "----------- build complted ----------"
            }
        }
        stage("test"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                 echo "----------- unit test Complted ----------"
            }
        }

    stage ('SonarQube analysis'){
        environment {
            scannerHome = tool 'saurabh-sonar-scanner'
        }
        steps{
            withSonarQubeEnv('saurabh-sonarqube-server'){
                sh "${scannerHome}/bin/sonar-scanner -x"
            }
        }
    }
    }
}
