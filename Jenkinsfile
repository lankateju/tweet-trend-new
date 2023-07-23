pipeline{
    agent { label 'slave-server' }
    environment{
        PATH = "/opt/apache-maven-3.9.3/bin:$PATH"
    }
    stages {
stage("build"){
          steps{
                sh 'mvn clean install'
            }
        }
        stage('test') {
        steps {
                    echo '-----unit test started--------'
                    sh 'mvn surefire-report:report'
                    echo '-----unit test completed--------'
                }
            }
            //
            stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'valaxy-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('valaxy-sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
            //
        stage("Quality Gate"){
            steps{
            script{
  timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
    def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
    if (qg.status != 'OK') {
      error "Pipeline aborted due to quality gate failure: ${qg.status}"
    }
  }
}
        }
        }
        //
        }
    }

