def registry = 'https://lanka.jfrog.io'
def imageName = 'lanka.jfrog.io/image-docker/image'
pipeline {
    agent {
        node {
            label 'slave-server'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.2/bin:$PATH"
}
    stages {
        stage("build"){
            steps {
                 echo "----------- build started ----------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                 echo "----------- build complted ----------"
            }
        }
    }
}

          
